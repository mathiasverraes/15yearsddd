# Type Safety and Money


<!-- photo credit http://s1153.photobucket.com/user/campbellchevelle/media/MoneyTree5_zpszzjjrpdw.jpg.html -->

Below is an attempt at illustrating a design/redesign process I went through at a client, who's started refactoring the core systems their business depends on. Design is the part of software development that is the most messy, the hardest to fit into rules or well-defined processes. In fact, while writing this post, I tweeted:

> ["There are surprisingly few software design books that recommend taking a walk, a shower, or a nap, as an important step."](https://twitter.com/mathiasverraes/status/704250689107709952)

None of the solutions offered below should be taken as truth. I may have already changed my mind on some of them by the time you read them. 

## History

In 2010, I wrote a small library with some Value Objects to represent money, and in 2011, I published a first version. It was a typical open source scratch-your-own-itch thing, that solved a problem with incorrect rounding and conversion in an e-commerce project I was working on. It seems to have scratched many itches, as it got quite popular.

I’ve been a bad parent to the project lately. It's in a [new GitHub organisation](https://github.com/moneyphp/money) now, with @sagikazarmark as the new maintainer, who's blowing new life into it.

Over the years, a bunch of forks and variations appeared. I welcomed this, as many of them serve a need that my library didn’t. It freed me from having to support all possible use cases, and avoided feature bloat. 


## Design Flaws

<img style="float:right;margin-left: 10px" src="/img/posts/2016-02-29-type-safety-and-money/MoneyTree-small.jpg" alt="MoneyTree">

Apart from being incomplete, the library suffers from fundamental design flaws, some of which can’t be fixed without breaking it.

- It doesn’t support higher precision than the currency’s default precision.
- As a result of this, it always rounds, so if you chain operations, you end up with rounding errors.
- It doesn’t support blockchain currencies, or virtual, vendor-specific currencies, like Facebook Credits (now discontinued), casino chips, game credit…
- Having to enter values in integers was often impractical (eg €1 had to be written as 100.)
- Some currencies have mills (1/1000<sup>th</sup> of a unit) as their official division (although they are becoming rare). Bitcoin supports 10<sup>−3</sup> (a millibitcoin), 10<sup>−6</sup> (a microbitcoin or a bit), and 10<sup>−8</sup> (a satoshi). Reportedly, the community is considering to introduce even smaller divisions. The library doesn't support any of this.

## Requirements

This is what we expect from our model:

1.	We need to support about 10 currencies, possibly more in the future. When we do add new currencies, it is assumed that the in-house developers will add support in the code. There’s no UI for adding new currencies.
2.	All operations need to done with a precision of 8 decimals. This is a business decision.
3.	When showing amounts to users, or pass them along over an API, we always stick to the currency’s official division. In the case of Bitcoin, that does indeed mean we’re keeping a precision of 1 satoshi aka BTC 10<sup>−8</sup>.
4.	In some markets, our software will need to do specific compliance reporting.
5.	All internal reporting needs to be in EUR, no matter what the original currency was.
6.	We’re using some legacy and third-party systems, that also publish revenues to our internal reporting tool. Most of them only support the currency’s official division, and can’t deal with higher precision.
	
## Assumptions
 
To understand this post, I'm assuming you know:

- what a Value Object is, and why you'd want some;
- how you can make your objects immutable;
- why they _should_ be immutable;
- how you can make operations safer, eg by disallowing $1+€1 without explicit conversion;
- why splitting €0.05 between two parties is not €0.025+€0.025 but €0.03+€0.02.

## Fowler-style

Let's design!
 
Our first instinct is to have the `Money` object from [Fowler's PoEAA](http://amzn.to/1TN7Tq4), consisting of a float<sup>*</sup> and a currency, which in turn could be an object as well. Both are immutable.

(<sup> * </sup> You may not want to use the actual float type in your programming language for dealing with money, as you may run into issues with precision. Do your research.)

<img style="float:right;margin-left: 10px" src="/img/posts/2016-02-29-type-safety-and-money/Money.png" alt="Money">

`Currency` is an enum type supporting our 10 currencies (A simple assertion will do if your language doesn't have enums). We can't initialise the `Currency` object with any other value than our 10 currencies. It only uses the 3-letter ISO symbols, anything else is an error. That satisfies requirement 1.

<img style="float:right;margin-left: 10px" src="/img/posts/2016-02-29-type-safety-and-money/MoneyFormatter.png" alt="MoneyFormatter">

`Money`’s constructor can round floats with more than 8 decimals. We can add some operations, like `add(Money other) : Money` and `multiply(float operand) : Money`. They also round to 8 decimals if needed. 


Requirement 3 (showing pretty-printed, rounded values to the users), is clearly presentation logic. We should avoid muddying up our domain model for this. So we add a `MoneyFormatter` in the presentation layer, which takes a `Money` argument and returns a string, such as €5.00 or 5,00€, depending on local standards. Perhaps we even make a HTML widget or helper of sorts, so that our templates don’t need to worry about it.



## Itch

Our current design doesn’t satisfy the problem of exposing the rounded values over an API. Of course, we could `round(money.getAmount())`, but `money.round() : Money` seems more in line with our existing methods. 

This is where you should start feeling the itch. Have a close look at the type of this method. `money.round() : Money`

{% highlight java %}
a = new Money(1.987654321, eur)
// The constructor rounds it own to 1.98765432
b = a.round()
// round() rounds it up to 1. 99 and instantiates a new Money
// Money’s constructor rounds it to 1.99000000
{% endhighlight %} 

Technically, most languages don’t distinguish between 1.99 and 1.99000000, but logically, there is an important nuance here. `b` is not just any `Money` , it is a fundamentally different type of money. Our design doesn’t make that distinction, and just mixes up money, whether it was rounded or not.

Let's make the implicit explicit. We can rename `Money` to `PreciseMoney`, and add a new type called `RoundedMoney`. The latter always rounds to whatever the currency's default division is.

The `round()` method now becomes very simple:

{% highlight java %}
PreciseMoney {
	round() : RoundedMoney {
		return new RoundedMoney(this.amount, this.currency)
     }
}
{% endhighlight %} 


The chief benefit is strong guarantees. We can now typehint against `PreciseMoney` in most of our domain model, and typehint against `RoundedMoney` where we explicitly want or need it. 

It's easy to underestimate how valuable this style of granular types can be.

- **It's defensive coding, against a whole category of bugs**. Methods and their callers now have an explicit contract, about what kind of money they are talking about. 
- **It's declarative coding**. Declarative style require a lot less tests. There's no point in testing something that is obviously correct. Code with an explicit contract like this, is obviously correct. This is why proponents of strong static type systems like to talk about *Type Driven Development* as an alternative to *Test Driven Development*. 
- **It communicates to different people working on the code, that we care specifically about the difference.**
- **It introduces a concept from the domain into the Ubiquitous Language and the model**. Before we did that, it would likely go unnoticed that terms like "precision" were in fact part of our language. Co-evolving the language, the models, and the implementation, is central to Domain-Driven Design. 
- This design also **helps to apply the Interface Segregation Principle**.

## Type Juggling
   
We're not building this as a generic library, so we don't need to supply a "complete" API. We can (and we should) only add the methods that we are actually going to use. In our case, `PreciseMoney` has a `round()`, but `RoundedMoney` has no `toPrecise()`. In other words, we can cast `PreciseMoney` to `RoundedMoney`, but we can't cast `RoundedMoney` to `PreciseMoney`. It's a one way operation. 

There's an elegance to that constraint. Once you round something, the precision is lost forever. The lack of `RoundedMoney.toPrecise()` fits our understanding of our domain.

Perhaps we'll eventually need some operations on `RoundedMoney`, (although I'd rather avoid having them). We can choose some smart return types: 

{% highlight java %}
RoundedMoney.add(RoundedMoney other) : RoundedMoney
RoundedMoney.multiply(Float operand) : PreciseMoney
{% endhighlight %} 

Notice the different return types. 

Perhaps you're writing some client code that wants to do multiplication, but doesn't care about high precision. Chaining methods would suffice here:

{% highlight java %}
someCash.multiply(0.3333).round()
{% endhighlight %} 

Again, this style is very explicit. The compiler or type checker can protect us when we make mistakes against the types, such as passing `PreciseMoney` when `RoundedMoney` is required.

## Conversions
   
Converting between different currencies depends on today's exchange rates. We'll need to fetch those from some third party web API. Or perhaps, another process is putting that information in a file or database somewhere. We don't want to leak that kind of detail into our model, so we can have an Exchange interface, and have one or more implementations of our choice. The method on that interface that we're interested in, takes a `PreciseMoney` and a target `Currency`, and does the conversion.

{% highlight java %}
interface Exchange {
   convert(PreciseMoney source, Currency target) : PreciseMoney
}
{% endhighlight %} 


The `Exchange` implementations will also need to deal with concerns such as caching today's rates, to avoid unnecessary traffic on each call. 

If fetching + caching + converting sounds like a lot of responsibility for one service, that's because it is (and this one is actually still very clean as compared to most service classes I see in actual code). These kinds of service classes are fundamentally procedural code wrapped in an object. Even though leakage is reduced thanks to the Exchange interface, the rest of our code still needs to depend on that interface. This makes testing harder, as all those tests will need to mock `Exchange`. And finally, (although I agree it's subtle here), all implementations of `Exchange` will need to duplicate the actual conversion, or somehow share code. A heuristic that helps, is to figure out if we can somehow isolate the side-effectful code (fetching, caching) from the domain logic (conversion). 

You guessed it, we need to identify a missing concept. Instead of having the `Exchange` do the conversion, we can make it return a `ConversionRate` instead. This is a Value Object that represents a source `Currency`, a target `Currency`, and a factor (a float). Value Objects attract behaviour, and in this case, it's the `ConversionRate` object that becomes the natural place for doing the actual calculation.

{% highlight java %}
interface Exchange {
   getRate(Currency source, Currency target) :: ConversionRate
}

ConversionRate {
  convert(PreciseMoney source) : PreciseMoney
}
{% endhighlight %}

The `convert` method makes sure that we never accidentally convert USD to EUR using the rate that was actually meant for GBP to BTC. All it needs to do is throw an exception if the arguments have the wrong currency.

The other cool thing here is that we don't need to pass around `Exchange`. Instead, we pass around the much smaller, simpler, `ConversionRate` objects. They are, once again, more composable. Already the possibilities for reuse become obvious: for example, a transaction log can store a copy of the `ConversionRate` instance that was used for a conversion, so you get accountability.

## Simpler Elements 

An `Exchange` is now something that represents the collection of `ConversionRate` objects, and provides access (and filters) on that collection. Sounds familiar? This is really just the *Repository* pattern! Repositories are not just for Entities or Aggregates, but for all domain objects, including Value Objects. 

(We could rename `Exchange` to `ConversionRateRepository`, which would make the pattern more explicit, but remove a name from our Ubiquitous Language. It's helpful in some contexts. Personally, I'd be more in favour of keeping the name. We can annotate `Exchange` as a @Repository, or have it implement a marker interface called `Repository`.)

We split up our procedural original `Exchange` service into the two simpler patterns, Repository and Value Object. Notice how we have at no point removed any essential complexity, and yet each element, each object, is very simple in its own right. To understand this code, the only pattern knowledge a junior developer would need, is in a few pages of chapters 5 & 6 of [Domain-Driven Design](http://amzn.to/1LrjmZF).

## Currency Type Safety
   
We still have some issues. Remember that some currencies have a division of 1/00, 1/1000, or 1/100000000. `RoundedMoney` needs to support this, in our case for 10 currencies. The constructor is starting to look pretty ugly:

{% highlight java %}
switch(currency) 
    case EUR: this.amount = round(amount, 2)
    case USD: this.amount = round(amount, 2)
    case BTC: this.amount = round(amount, 8)
etc
{% endhighlight %} 

Every time we need to support a new currency, we need to add code here, and possibly in other places in our system. Not a serious issue, but not ideal. A switch statement is often a smell for missing types. (Yes, we could replace this with a map, but it's really the same thing. And a map wouldn't fit if we'd be dealing with more interesting behavioural differences between currencies than rounding.)

What happens if we make `PreciseMoney` and `RoundedMoney` abstracts or interfaces, and factor the variation out into subtypes for each currency? 

<img src="/img/posts/2016-02-29-type-safety-and-money/FactorOutCurrency.png" alt="Factoring out currency">

Each of the `PreciseEUR`, `PreciseBTC`, `RoundedEUR`, `RoundedBTC` etc classes have very local knowledge about how they go about their business, such as the rounding switch example above.

{% highlight java %}
RoundedEUR {
   RoundedEUR (amount) {
       this.amount = round(amount, 2)
   }
}
{% endhighlight %}

Again, we can put the type system to work here. Remember that, per requirement 5, our reporting needs to be in EUR? We can now typehint for that, making it impossible to pass any other currency into our reporting. Similarly, the different compliance reporting strategies we need for requirement 4 can each be limited to the currencies they support.

Sure, we get a bit of class explosion. But so what? It's much preferable to long methods.


## Minimalist Interfaces

A benefit of having lots of small classes, is that we can get rid of a lot of code. Perhaps our main Bounded Context deals with the 10 `PreciseXYZ` types, but our Reporting Bounded Context only supports `RoundedEUR`. That means there's no need to support `RoundedUSD` etc, as we are not using it. This also implies that we don't need `round()` methods on any of the `PreciseXYZ` classes, apart from EUR. Less code means less boilerplate, less bugs, less tests, and less maintenance.

Not supporting a way back from `RoundedEUR` to `PreciseEUR` is another example of a minimalist interface. Don't build behaviours that you don't need or want to discourage.

## Single Responsibility

Another benefit of these small, ultra-single-purpose classes, is that they very rarely need to change. This is Robert C. Martin's heuristic for the Single Responsibility Principle: 

> "A class should have only one reason to change."

A good design allows you to easily add or remove elements, or change the composition of the elements, but rarely requires you to actually change existing code. This in turn leads to fewer bugs and less work. 


## Parent interface?

You may have noticed that in the current design, I have no `Money` interface at the top of the object graph. Aren’t `PreciseMoney` and `RoundedMoney` both a kind of `Money`? Don’t they share a lot of methods?

If we are trying to build a model inspired by the real-world, this would make sense. However, we shouldn’t judge our models by how well they fit our hierarchical categorisations. We judge our models by usefulness. A top-level `Money` interface adds no value at all; in fact it takes away value. 

<img style="float:right;margin-left: 10px" src="/img/posts/2016-02-29-type-safety-and-money/BadMoney.png" alt="Bad Money">

This may be a bit counterintuitive. `PreciseMoney` and `RoundedMoney`, although somewhat related, are fundamentally different types. We’ve designed our model for clarity, for the guarantee that we don’t mix up rounded and precise values. By allowing client code the typehint for the generic Money, we’ve taken away that clarity. There’s now no way of knowing which we’re getting. All responsibility for passing the correct type is now back in the hands of the caller. 


## Overdesign 

Is this overdesigned? Perhaps, depending on your context. When you only want to display some prices, it's likely overkill. With code that decides about huge amounts of money, a design like this helps me sleep at night. 

There's a hint in the language. We don't say "this thing is designed", we say "this thing is designed for **that purpose**". Overdesign (and underdesign) simply mean "not designed for purpose", or "designed for a different purpose than the current one". The model presented here is designed for the purpose of high precision and confidence in our operations with money.

Often, different aspects of our system have different requirements. This is precisely what Bounded Contexts are for: allow us to reason about our system as a a number of cooperating models, as opposed to one unified model. Perhaps our Product Catalog needs a really simple model for money, because it doesn't really do anything other than displaying prices. Sales and Reporting on the other hand might benefit from our more intricate design.

<img src="/img/posts/2016-02-29-type-safety-and-money/Hexagonal.png" alt="Hexagonal">

## Practicality
   
It’s important to distinguish between “overdesigned” and “impractical”. The solution to overdesign is to remove elements, make it simpler until it just fits. The solution to impracticality, can be to add more abstractions and shortcuts. 

{% highlight java %}
new PreciseMoney(5.00, new Currency(EUR))
{% endhighlight %} 

is a handful to write. There’s no reason why you shouldn’t add a static factory method, like

{% highlight java %}
PreciseMoney.EUR(5.00)
{% endhighlight %} 

Or just a naked function if your language supports it

{% highlight java %}
EUR(5.00)
{% endhighlight %} 

Or a unicode function

`€(5.00)`

(Unfortunately, $ is used in many languages to mean all kinds of things, none of which are USD. Be creative!)

## Defensive model

There is of course no way to defend your code against bad coders. Unless you’re doing [code reviews](/2013/10/pre-merge-code-reviews/), someone could change the Value Objects to be mutable, and delete the tests. (Funny story: I was once told that the new developer hired to replace me after I left a job, replaced all private methods by public ones, “because it’s more convenient”.) 

I do believe though that good design communicates intent. No matter the level of the developers using your code, if they see two types for rounded and precise money, chances are they are at least going to consider that perhaps we can’t just mix the two in operations without thinking about it.


## Going Further

<img style="float:right;margin-left: 10px" src="/img/posts/2016-02-29-type-safety-and-money/Price.png" alt="Price">

Value Objects are the ultimate composable objects, so we can keep looking for implicit concepts that we can make explicit. For example, we can naively use our money type to represent prices. But what if a price is not so simple? Maybe `Price` is composed of a `PreciseMoney` and a `VATRate` or `Tax` object of sorts. Maybe a `ProductPrice` is composed multiple `Price` objects for different amounts, for example  if you offer a discount when buying in bulk. 

Value Objects make it easy to build abstractions that can handle lots of complexity at a very small cognitive cost to the developer using it. Finding the abstractions can be costly and hard, but spending the effort here usually impacts code quality and maintainability so much in the long run, that it's very often worth it.


## Timezone Type Safety

The concept of using the type system to reduce a whole classes of errors in code without resorting to excessive tests, can be applied to many domains. Recently, I was late for a talk I was doing at a meetup in London, because a certain website's "Export to Google Calendar" feature didn't take timezones into account. Timezone bugs are not only a nuisance to a regular traveler like myself, but can have dire consequences. 

Haskell's Time library has separate types for `UTCTime` and `ZonedTime`, and offers functions to convert between them. This gives guarantees from the compiler that a programmer can not easily mix them up, or implicitly converts between them. Ideally, your code should use `UTCTime` everywhere, and only convert to and from `ZonedTime` when human users are involved. It should be easy enough to build something like this in object oriented languages.

## Conclusion

In many environments, dealing with money is too critical to be regarded as a Generic Subdomain. Different projects have different needs and expectations of how money will be handled. If money matters, you need to build a model that fits your specific problem space like a glove. Some of the tools in our belt are small composable building blocks, making the implicit explicit, and using the type system to our advantage. You might end up with something entirely different.

*All good design is redesign.*





