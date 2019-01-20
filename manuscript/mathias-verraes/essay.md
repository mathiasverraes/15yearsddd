# Emergent Contexts through Refinement — Mathias Verraes

Which Bounded Context owns a particular concept? One way to find out is by evolving your model until everything finds a natural place. All models are wrong, especially the early ones. Let's look at some simple requirements, and explore how we can evolve the model over time. As we learn more about the problem we're solving, we can bring that clarity into new iterations of the model. 

## The problem

Imagine working on a business application, that deals with sales, accounting, reporting, that sort of thing. The existing software has some serious issues. For example, monetary values are represented as scalars. In many places, values are calculated at a high precision, and then rounded down to 2 decimals, and later used again for high precision calculations. These rounding errors are all over the code. It doesn't make a huge difference on a single amount and a single rounding error, but eventually it could add up, and cost the business millions. The monetary values can represent different currencies, but the financial reporting is always in EUR. It is unclear if the code always correctly converts to EUR when needed, or accidentally adds up amounts from different currencies.

To solve these problems, the first thing to do is to have conversations with the domain experts from sales and accounting. As a result, we can come to a common agreement on some requirements.
    
## Requirements

1.    Business needs to support about 10 currencies, possibly more in the future. When business wants to support a new currency, say Japanese Yen, then it is assumed that the developers will add support in the code. There’s no need for a UI for adding new currencies.
2.    All price calculations need to be done with a precision of 8 decimals. This is a business decision.
3.    When showing amounts to users, or passing them along over an API, the software will always stick to the currency’s official division. For example, in the case of EUR or USD, that's 2 decimals. In the case of Bitcoin, a precision of 1 satoshi aka BTC 10^-8^. 
4.    In some markets, the software will need to do specific compliance reporting. 
5.    All internal reporting needs to be in EUR, no matter what the original currency was.
6.    There will be some legacy and third-party systems, that also publish revenues to the internal reporting tool. Most of them only support the currency’s official division, and can’t deal with higher precision.

I> Some programming languages don't deal well with highly precise calculations. There are workarounds which won't be discussed in this article. Just assume that here "number" means a suitable datatype, such as float or Decimal in C# or BigDecimal in Java.

## The first step

Are there existing design patterns that can help here? A good pattern to apply when dealing with monetary values is the Value Object pattern from [Domain-Driven Design](http://amzn.to/1CdXXP9). 
In fact, a couple of years before Eric Evans published his book, Martin Fowler described an implementation for `Money` in [Patterns of Enterprise Application Architecture](http://amzn.to/1TN7Tq4). 
The pattern describes an object consisting of two properties, a number for the amount, and another property for the associated currency (which could be a Value Object as well). The `Money` Value Object is immutable, so all operations will return a new instance.

![Figure 1](images/mathias-verraes/Money.png)

The `Currency` type supports the 10 different currencies that the business is interested in. Enums can be used, but a simple assertion will do if the language doesn't have support for enums. The following constraints can be added:

- The type can't be initialised with a value different from any of the supported 10 currencies. 
- It only uses the 3-letter ISO symbols, anything else is an error. That satisfies requirement 1.


`Money`’s constructor rounds the numbers to 8 decimals. This gives it enough precision to deal with any currency. Operations like `Money.add(Money other) : Money` and `Money.multiply(Number operand) : Money` etc can be added to the `Money` class. The operations automatically round to 8 decimals. In addition, there's also a `Money.round() : Money` method that returns a new Money object, rounded to 2 decimals. 

{lang="java"}
    Money {
        // ...
        round() : Money {
            return new Money(round(this.amount, 2), this.currency)
         }
    }


Now that we have modeled the types based on the requirements, the next step is to refactor all the places in the old code that do things with money to use the new `Money` object.

## Composition

An interesting aspect of Value Objects, is that they are the ultimate composable objects. That helps to make implicit concepts more explicit. For example, we could naively use the money type to represent prices. But what if a price is not so simple? In Europe, prices have a Value Added Tax component. You can now naturally compose a new `Price` Value Object from a `Money` and a `VAT` object, the latter representing a percentage.

![Figure 2](images/mathias-verraes/Price.png)

A Product could have different prices in different markets, and we can make this concept explicit in a another Value Object.

![Figure 3](images/mathias-verraes/ProductPrice.png)

... and so on. We can push a lot of logic that we'd traditionally put in services, down into these Value Objects. 

Value Objects make it easy to build abstractions that can handle lots of complexity, at a low cognitive cost to the developer using it. Finding the abstractions can be hard, but spending the effort here usually impacts code quality and maintainability so much in the long run, that it's very often worth it.


   
## Look for weaknesses
 
Even if the current model feels intuitively good, there is always room for improvement. Eric often suggests to look for aspects that are awkward or painful to use. These are smells, pointing to opportunities for further refinement.

Looking closely at the model, there are two potential weaknesses: 

1. While the scalars in the code have been replaced by the `Money` type, the software is still at risk that money is being rounded and then reused in a higher precision calculation. This problem of rounding errors still has not been fully addressed.
2. The software supports 8 decimal precision only, and the model assumes this is fine. However, when `Money.round()` gets invoked, the model doesn't really deal well with the fact that some currencies don't have two but three decimals by default (such as Bahraini and Kuwaiti Dinar) or more (like Bitcoin), and some have none (like the Japanese Yen).

This is where we should start feeling an itch to stop and rethink our model. 

Have a close look at: `Money.round() : Money`

{lang="java"}
    a = new Money(1.987654321, eur)
    // The constructor rounds it down to 1.98765432
    b = a.round()
    // round() rounds it up to 1.99 and instantiates a new Money
    // Money’s constructor rounds it to 1.99000000


Technically, most programming languages don’t distinguish between 1.99 and 1.99000000, but logically, there is an important nuance here. `b` is not just any `Money` , **it is a fundamentally different type of money**. The current design doesn’t make that distinction, and just mixes up money, whether it was rounded or not.

## Make the implicit explicit. 

A good heuristic when modelling, is to consider if we can be more explicit in the naming, and tease out subtly different concepts. We can rename `Money` to `PreciseMoney`, and add a new type called `RoundedMoney`. The latter always rounds to whatever the currency's default division is.  

The `Money.round()` method now becomes very simple:

{lang="java"}
    PreciseMoney {
        round() : RoundedMoney {
            return new RoundedMoney(this.amount, this.currency)
         }
    }

![Figure 4](images/mathias-verraes/PreciseMoney.png)


The chief benefit is strong guarantees. We can now typehint against `PreciseMoney` in most of our domain model, and typehint against `RoundedMoney` where we explicitly want or need it. 


It's easy to underestimate how valuable this style of granular types can be.

- **It's defensive coding, against a whole category of bugs**. Methods and their callers now have an explicit contract, about what kind of money they are talking about. Good design communicates intent.
- **Contracts beat tests**. Obviously correct code doesn't need tests. If `RoundedMoney` is well-tested, and some client code typehints for that type, we don't need a test to verify that this money is in fact rounded. This is why proponents of strong static type systems like to talk about *Type Driven Development* as an alternative to *Test Driven Development*: Declare your intent through types, and have the type checker do the work. 
- **It communicates to different people working on the code, that we care specifically about the difference.** A developer who is unfamiliar with this problem space, might look for a `Money` type. But the IDE tells them no such type exists, and suggests `RoundedMoney` and `PreciseMoney`. This forces the developer to consider which type to use, and learn something about how the domain deals with precision.
- **It introduces a concept from the domain into the Ubiquitous Language and the model**. Precision and Rounding was fundamental to the domain but clearly ignored in the original model. Co-evolving the language, the models, and the implementation, is central to Domain-Driven Design. These model refinements can have exponential payoffs in the long run.
- This design also **helps to apply the Interface Segregation Principle**. Client code will not depend on an large set of APIs, only on the ones relevant to the type.

## Dealing with different precision
   
We can add a `round()` method to `PreciseMoney`, but we wouldn't add a `toPrecise()` method to `RoundedMoney`. Just like in physics, we can't create more precision out of nothing. In other words, you can cast `PreciseMoney` to `RoundedMoney`, but you can't cast `RoundedMoney` to `PreciseMoney`. It's a one way operation. 

There's an elegance to that constraint. Once you round something, the precision is lost forever. The lack of `RoundedMoney.toPrecise()` fits the understanding of the domain. 

## Common Interfaces

You may have noticed that in the current design, there is no `Money` interface at the top of the object graph. Aren’t `PreciseMoney` and `RoundedMoney` both a kind of `Money` or `AbstractMoney`? Don’t they share a lot of methods?

If the goal is to try and build a model inspired by the real-world, this would make sense. However, don't judge your models by how well they fit into hierarchical categorisations. A Domain Model is not an taxonomy — in contrast to the OOP books that teach you that a `Cat extends Animal`. Judge your models based on usefulness instead. A top-level `Money` interface adds no value at all; in fact it takes away value. 

![Figure 5](images/mathias-verraes/BadMoney.png)


This may be a bit counterintuitive. `PreciseMoney` and `RoundedMoney`, although somewhat related, are fundamentally different types. The model is designed for clarity, for the guarantee that rounded and precise values are not mixed up. By allowing client code the typehint for the generic `Money`, you've taken away that clarity. There’s now no way of knowing which `Money` you're getting. All responsibility for passing the correct type is now back in the hands of the caller. The caller could do `money instanceof PreciseMoney`, but that's a serious code smell.

## Dealing with Conversions
      
Converting between different currencies depends on today's exchange rates. The exchange rates probably come from some third party API or a database. To avoid leaking these technical details into the model, we can have an `CurrencyService` interface, with a `convert` method. It takes a `PreciseMoney` and a target `Currency`, and does the conversion.

{lang="java"}
    interface CurrencyService {
       convert(PreciseMoney source, Currency target) : PreciseMoney
    }

The `CurrencyService` implementations might deal with concerns such as caching today's rates, to avoid unnecessary traffic on each call. 

If fetching + caching + converting sounds like a lot of responsibility for one service, that's because it is. Service classes like are `CurrencyService` fundamentally procedural code wrapped in an object. Even though leakage is reduced, thanks to the `CurrencyService` interface, the rest of the code still needs to depend on this interface. This makes testing harder, as all those tests will need to mock `CurrencyService`. And finally, all implementations of `CurrencyService` will need to duplicate the actual conversion, or somehow share that logic. A heuristic that helps, is to figure out if we can somehow isolate the actual domain logic code from the part of the code that is just trying to prepare the data for the domain logic to be applied. For example, differentiate the domain logic (conversion) from the infrastructure code (fetching, caching). 

There's a missing concept here. Instead of having the `CurrencyService` do the conversion, we can make it return a `ConversionRate` instead. This is a Value Object that represents a source `Currency`, a target `Currency`, and a factor (a float). Value Objects attract behaviour, and in this case, it's the `ConversionRate` object that becomes the natural place for doing the actual calculation.

{lang="java"}
    interface CurrencyService {
        getRate(Currency source, Currency target) :: ConversionRate
    }
    ConversionRate {
        - sourceCurrency : Currency 
        - targetCurrency : Currency
        - factor : Float
        convert(PreciseMoney source) : PreciseMoney
    }



The `convert` method makes sure that we never accidentally convert USD to EUR using the rate that was actually meant to convert GBP to JPY. It can throw an exception if the arguments have the wrong currency.

The other cool thing here is that there's no need to pass around `CurrencyService` interface. Instead, we pass around the much smaller, simpler, `ConversionRate` objects. They are, once again, more composable. Already the possibilities for reuse become obvious: for example, a transaction log can store a copy of the `ConversionRate` instance that was used for a conversion, so we get accountability.

## Simpler Elements 

An `CurrencyService` is now something that represents the collection of `ConversionRate` objects, and provides access (and filters) on that collection. Sounds familiar? This is really just the *Repository* pattern! Repositories are not just for Entities or Aggregates, but for all domain objects, including Value Objects. 

We can now rename `CurrencyService` to `ConversionRateRepository`. It has the benefit of being more explicit, and more narrowly defined. Having the pattern name `Repository` in the class name is a bit of an annoyance. And we should take the opportunity to look for terms in the Ubiquitous Language. A place where you can get today's conversion rates, is a foreign exchange, so we can rename `ConversionRateRepository` to `ForeignExchange` or `Forex`. Rather than put the word Repository in the classname, we can annotate `ForeignExchange` as a @Repository, or have it implement a marker interface called `Repository`.

The original procedural `CurrencyService` is now split into the two simpler patterns, Repository and Value Object. Notice how we have at no point removed any essential complexity, and yet each element, each object, is very simple in its own right. To understand this code, the only pattern knowledge a junior developer would need, is in a few pages of chapters 5 & 6 of [Domain-Driven Design](http://amzn.to/1LrjmZF). 

## Currency Type Safety
   
There are still have some issues left. Remember that some currencies have a division of 1/00, 1/1000, or 1/100000000. `RoundedMoney` needs to support this, and in this case, for 10 different currencies. The constructor can start to look somewhat ugly:

{lang="java"}
    switch(currency) 
        case EUR: this.amount = round(amount, 2)
        case USD: this.amount = round(amount, 2)
        case BTC: this.amount = round(amount, 8)
    etc


Also, every time business needs to support a new currency, new code needs to get added here, and possibly in other places in the system. While not a serious issue, it's not exactly ideal either. A switch statement (or a key/value pairs) can be a smell for missing types.

One way to achieve this is to make `PreciseMoney` and `RoundedMoney` abstracts or interfaces, and factor the variation out into subtypes for each currency.

![Figure 6](images/mathias-verraes/FactorOutCurrency.png)

Each of the `PreciseEUR`, `PreciseBTC`, `RoundedEUR`, `RoundedBTC` etc classes have local knowledge about how they go about their business, such as the rounding switch example above.

{lang="java"}
    RoundedEUR {
       RoundedEUR (amount) {
           this.amount = round(amount, 2)
       }
    }

Again, we can put the type system to work here. Remember the requirement that the reporting needs to be in EUR? We can now typehint for that, making it impossible to pass any other currency into our reporting. Similarly, the different compliance reporting strategies for different markets can each be limited to the currencies they support.

So, when should you _not_ want to lift values to types?

Let's say you're not dealing with 5 or 10 values, but there is an infinite or very large set of potential values. Or when you're expecting each of these implementations to change often. In this case, having to support 10 currencies is somewhat on the edge. But again, it's very unlikely that you're having to add support for all 180 currencies. You're probably going to only support the 10 or 15 most relevant ones.  

## Minimalist Interfaces

A benefit of having lots of small classes, is that we can get rid of a lot of code. Perhaps the Sales Bounded Context deals with the 10 `PreciseXYZ` types, but the Reporting Bounded Context only supports `RoundedEUR`. That means there's no need to support `RoundedUSD` etc, as there's no need for it. This also implies that we don't need `round()` methods on any of the `PreciseXYZ` classes, apart from EUR. Less code means less boilerplate, less bugs, less tests, and less maintenance.

Not supporting a way back from `RoundedEUR` to `PreciseEUR` is another example of a minimalist interface. Don't build behaviours that you don't need or want to discourage.

## Single Responsibility

Another benefit of these small, ultra-single-purpose classes, is that they very rarely need to change, and only when something in the domain changes. Currencies are very stable concepts, and our model mimics this slow rate of change. A good design allows you to easily add or remove elements, or change the composition of the elements, but rarely requires you to actually change existing code. This in turn leads to fewer bugs and less work and more maintainable code. 


## Ledger

One advantage of expressing our code in terms of rich, well-adapted domain models, is that sometimes this can lead to finding opportunities for other features. It also makes the implementation of those features very easy. 

In this case, the whole point of this modelling exercise was to solve the precision problem. Every time a precise value is rounded, what happens to the fractions of cents that the business gains or loses? Is this important to the domain?

If so, we can keep a separate ledger for rounding. Every time a fraction of the value is gained or lost by rounding, we record it in the ledger. When the fractions add up to more than a cent, we can add it to the next payment. 

{lang="java"}
    // rounding now separates the rounded part from the leftover fraction
    PreciseMoney.round() : (RoundedMoney, PreciseMoney)
    Ledger.add(PreciseMoney) : void

You might not have to deal with this in most domains, but when you have high volumes of small transactions, it could make a significant difference. Consider this a pattern for your toolbox.

The point here is that our model is easy to extend. In the original code, where rounded and precise amounts were not clear, keeping track of lost fractions of cents would have been a nightmare. Because the change in requirements is reflected in the types, we can rely on the type checker to find all places in the code that need to be adapted. 


## Refining Bounded Contexts

Different capabilities of the system have different requirements. This is what Bounded Contexts are good for: they allow us to reason about the system as a number of cooperating models, as opposed to one unified model. Perhaps the Product Catalog needs a really simple model for money, because it doesn't really do anything other than displaying prices. Sales may need precise price calculations. Our internal Reporting might be fine with reporting with rounded numbers, or even with reporting with no decimals. Company financials are sometimes expressed in thousands or millions. The Compliance Reporting again has different needs.

![Figure 7](images/mathias-verraes/Contexts.png)

Cleaning up the language: 

![Figure 8](images/mathias-verraes/Contexts2.png)


If the Sales context always deals with high precision, does it then make sense to call the type `PreciseMoney`? Why not just `Money`? It should then be clearly understood that in the Sales Ubiquitous Language, there is only one `Money` and it doesn't tolerate rounding. In the Reporting Context, money is always rounded and in EUR. Again the type doesn't have to be `RoundedMoney` or `RoundedEUR`, it can just be `Money`.  

Every Bounded Context now gets its own domain models for Money. Some are simple, some have more complexity. Some have more features, others have less. We've already written all that code, we're just separating it into the Contexts where we need it. Each Bounded Context has a small, unique model for Money, highly adapted to its specific needs. A new team member working on a Bounded Context can now learn this model quickly, because it's unburdened by the needs of other Contexts. And we can rest assured that they won't make rounding errors or swap EUR and USD. Different teams don't need to coordinate on the features of Money, and don't need to worry about breaking changes. 

In some environments, a single Generic Subdomain for money would have been perfectly fine. In others, we want highly specialized models. Determining which is which is your job as a domain modeller.  

**We didn't do upfront analysis of what goes into which Bounded Context. If we had tried that, early on in the project, we would have naively built a shared Money library, assuming that the concept of Money is universal between all Contexts. Instead, we kept on refining our model based on our needs and new insights, and saw how these explicit concepts naturally found a place. Cultivate a healthy obsession with language, and keep refactoring towards deeper insight, one step at a time. All good design is redesign.**
