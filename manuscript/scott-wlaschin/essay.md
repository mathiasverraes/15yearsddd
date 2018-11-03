# Domain Modeling with Algebraic Data Types (by Scott Wlaschin)

*Authors note: It is a privilege to be able to contribute to this project. Even though it has been fifteen years since 'Domain Driven Design' was published, its insights and wisdom are just as valuable as ever, and continue to influence each new generation of programmers. One thing that has changed since it was written is the rise of functional programming as an alternative paradigm to object-oriented programming. Many articles on functional programming focus on the mathematical aspects, but I believe it has great potential for design, and can be used very effectively with DDD principles. This chapter explains why.*

One of the main aims of Domain Driven Design is to promote good communication between the development team, domain experts, and other stakeholders.
In particular, there should be a very close correspondence between the mental model of the domain experts and the code used in the implementation.
That is, if the domain expert calls something an "Order" then we should have something called an "Order" in the code that behaves the same way.
And conversely, we should avoid having things in our code that do *not* represent something in the domain expert's model. That means no terms like "OrderFactory",
"OrderManager", "OrderHelper", etc. A domain expert would not know what you mean if they saw these! Of course, some technical terms will have to occur in the codebase, but we should avoid exposing them as part of the design.

So the challenge is: how well can we create code that matches the domain? Can we create code that reads like text and is understandable by non-developers? And can we avoid introducing non-domain terms like "Manager" and "Factory".
I think we can do all of these things by using *algebraic data types* for domain modeling.

## Discovering common concepts in domain modeling

When we talk to domain experts during a discovery phase, we will encounter verbal descriptions of the domain such as these:

* "An order line has an order id, a product id, and an order quantity."
* "Contact information consists of a personal name and a contact method, where a contact method is either an email address or a phone number."
* "An email is either validated or unvalidated. Password resets should only be sent to validated emails."
* "A purchaser is either a one-time 'guest' or has been registered on the website. A registered purchaser has been given a customer id, which a guest doesn't have."
* "To pay for an invoice, you start with an unpaid invoice and payment information, and you end up with a paid invoice."

As we build our Ubiquitous Language from these discussions, there are some common patterns that occur, which we classify as follows:

* Primitive values
* Groups of things treated as one 
* Choices between things (values are 'or'ed together)
* Workflows (a.k.a. use-cases, scenarios, etc)
* States and lifecycles

Let's look at each of these in more detail.

### Primitive values

Domain experts will never talk about "integers" or "strings". Instead, they will use domain concepts such as "order quantity" or "email address".

These concepts may be *represented* by an integer or string, but they are not equivalent. For example, an "order id", a "product id", and an "order quantity" may all be represented by integers, but the domain concepts are in no way equivalent to an integer. It doesn't make sense to multiply a product id by two, for example. 

And even concepts which *are* integers don't correspond to a programmers `int` -- there are almost always constraints. For example, an "order quantity" must be one or more, and probably has an upper bound as well, such as 100. It's unlikely that a sales system would let you order 2 billion items!

Similarly an "email address" and a "phone number" might both be represented by strings, but again they are not interchangeable, and each will have special constraints.

If we were to document some of these primitive values, we might make notes like this:

```
data OrderId              // opaque -- don't care about representation
data ProductId            // opaque -- don't care about representation
data OrderQuantity is int // constrained to be between 1 and 100

data PersonalName is string // Must not be null or empty. Must be less than 100 characters.
data EmailAddress is string // Must not be null or empty. Must contain @ symbol.
data PhoneNumber is string  // Must not be null or empty. Must only contain digits, parens or hyphen.
```

When we come to translate these notes into code, we will want to preserve the simplicity of these descriptions.
The code should represent the domain as closely as possible.

### Groups of things treated as one thing

Of course, some domain values are not primitive, but are composed of other smaller values.
To document these kinds of things, we might make notes using "AND" to group the values together, like this:

```
data OrderLine = OrderId AND ProductId AND OrderQuantity
data ContactInformation = PersonalName AND ContactMethod
```

## Choices between things

Another common pattern is that a concept is comprised of alternatives.

* "An email is either validated or unvalidated"
* "A purchaser is either a one-time 'guest' or a registered customer"
* "An invoice is either unpaid or paid"

For these cases, we could use "OR" in our notes, like this:

```
data Email = UnvalidatedEmail OR ValidatedEmail
data ContactMethod = EmailAddress OR PhoneNumber
data Purchaser = GuestPurchaser OR RegisteredPurchaser (contains CustomerId)
data Invoice = UnpaidInvoice OR PaidInvoice
```

It's important to realize that these alternatives often play a critical role in business rules. For example:

* A password reset link should only be sent to a `ValidatedEmail` (never an `UnvalidatedEmail`).
* Discounts should only be given to a `RegisteredPurchaser` (never a `GuestPurchaser`).
* You can only apply a payment to an `UnpaidInvoice` (never a `PaidInvoice`).

Failing to clearly distinguish between these kinds of choices results in at best, a confusing design, and at worse, seriously defective implementations.

### Fighting the impulse to do class-driven design

One of the key tenets of Domain Driven Design is *persistence ignorance*. It is an important principle because it forces you to focus on modeling the domain accurately, without worrying about the representation of the data in a database.

Indeed, if you're an experienced object-oriented developer, then the idea of not being biased to a particular database model will be familiar, Object-oriented techniques such as dependency injection encourage you to separate the database implementation from the business logic.

But we also have to be careful of introducing bias into the design if we think in terms of objects and classes rather than the domain.
For example, as the domain expert describes the different kinds of contact methods, you may be tempted to create a class hierarchy in your head, like this:

```
class ContactMethodBase ...
class EmailAddressContactMethod extends ContactMethodBase ...
class PhoneNumberContactMethod extends ContactMethodBase ...
```

But letting classes drive the design can be just as dangerous as letting a database drive the design -- again, we're not really listening to the requirements!

* In our mental class hierarchy we have introduced an artificial base class, `ContactMethodBase`, that doesn't exist in the real world. This is a distortion of the domain. Try asking the domain expert what a `ContactMethodBase` is! 
* And similarly, an `EmailAddress` is a reusable primitive value, not specific to contact methods, so to use it in this particular context we have had to create a
wrapper class `EmailAddressContactMethod`. Again, this is another artificial object in the code that does not represent something in the domain.

The lesson here is that we should keep our minds open during requirements gathering and not impose our own technical ideas on the domain.

### Workflows

So far, we've been talking about "nouns" in our domain -- the data. 
In practice though, data structures are not the most important thing to model. Why is that?

A business doesn't just *have* data, it *transforms* it somehow. That is, you can think of a typical business process as a series of data or document transformations. The value of the business is created in this process of transformation, so it is critically important to understand how these transformations work and how they relate to each other.

Static data -- data that is just sitting there unused -- is not contributing anything. So what causes a person (or automated process) to start working with that data and adding value?
Often it's an outside trigger (a piece of mail arriving or your phone ringing), but it can also be a time-based trigger (you do something every day at 10 a.m.) or an observation (there are no more orders in the inbox to process, so do something else).

Whatever it is, it's important to capture it as part of the design. We generally call these things *Domain Events*. Domain Events are the starting point for almost all of the business processes we want to model. For example:

* "payment received" is a Domain Event that will kick off the "applying payment" workflow
* "email validation link clicked" is a Domain Event that will kick off the "validate email" workflow

There are number of ways to discover events in a domain, but one which is particularly suitable for a DDD approach is *Event Storming*, a collaborative
process for discovering business events and their associated workflows which was developed by Alberto Brandolini. 

So, given that we have discovered the events of interest, we next need to document the workflows (or use-cases) that are triggered by the events.
To keep things at a high level, we will just document what the inputs and outputs are for each workflow, like this:

```
workflow ApplyPaymentToInvoice =  
   triggered by: PaymentReceived
   inputs: UnpaidInvoice, Payment
   outputs: PaidInvoice    
   
workflow ValidateEmail  =
   triggered by: EmailValidationLinkClicked
   inputs: UnvalidatedEmail, ValidationToken (from clicked link)
   outputs: ValidatedEmail OR an error
```

In the second case, the validation might fail (e.g. the link has expired) and so the output is written as *choice* between alternatives: a validated email address, or an error.


### States and lifecycles

Most important business entities have a lifecycle -- they go through a series of changes over time. 

* An invoice starts off as unpaid, and then transitions to being paid.
* A purchaser starts off as a guest, and then transitions to being registered.

Even simple values can go through state transitions. For example, an email address starts off as unvalidated, and then transitions to being validated.

Being able to capture the states and transitions is an important part of domain modeling. To do this, we can use the same techniques described above: 
a set of choices to represent the various states, and workflows that transition between the states.
For example, for invoices, we can document the states and transitions like this:

```
// two states
data Invoice = UnpaidInvoice OR PaidInvoice

// one transition
workflow ApplyPaymentToInvoice = 
    transforms UnpaidInvoice -> PaidInvoice
```

In this case, there is no way to transition from `PaidInvoice` to `UnpaidInvoice`. Should there be? Thinking in terms of states and lifecycles is a great way to trigger productive design discussions.

## Understanding algebraic data types

Now that we've looked at some common concepts in domain modeling, let's look at how they can be mapped into code using algebraic data types.

In this section, we'll define what *algebraic data types* are. And then in the next section, we'll see how they can be used to capture our domain model.

### What are algebraic data types?

In an algebraic type system, new types are built from smaller types in two ways:

* By _AND_ing them together
* By _OR_ing them together

But what does _AND_ing and _OR_ing mean?

### "AND" Types

Let's start with building types using _AND_. For example, we might say that to make fruit salad you need an apple _AND_ a banana _AND_ some cherries.
This kind of type is familiar to all programmers. It is a *record* or *struct*. Functional programmers call this a *product type*.

Here's how the definition of a `FruitSalad` record type would be written in F#:

```
type FruitSalad = {
  Apple : AppleVariety
  Banana : BananaVariety
  Cherries : CherryVariety
}
```

The curly braces indicate that it is a record type, and the three fields are `Apple`, `Banana`, and `Cherries`.
The value in the `Apple` field must be of type `AppleVariety`, the `Banana` value must be of type `BananaVariety`, and so on.


### "OR" Types

The other way of building new types is by using _OR_. For example, we might say that for a fruit snack you need an apple _OR_ a banana _OR_ some cherries:
Functional programmers call this a *sum type* or *discriminated union*. I will call them *choice types* because they are used to represent choices in our domain.

Here's the definition of a `FruitSnack` using a choice type in F#:

```
type FruitSnack =
  | Apple of AppleVariety
  | Banana of BananaVariety
  | Cherries of CherryVariety
```

A vertical bar separates each choice, and the tags (such as `Apple` and `Banana`) are needed because sometimes the two or more choices may have the same type and so tags are needed to distinguish them. It can be read like this:

* A `FruitSnack` is either an `AppleVariety` (tagged with `Apple`) _OR_ a `BananaVariety` (tagged with `Banana`) _OR_ a `CherryVariety` (tagged with `Cherries`).

The varieties of fruit are themselves defined as choice types, which in this case is used similarly to an `enum` in other languages.

```
type AppleVariety =
  | GoldenDelicious
  | GrannySmith
  | Fuji
  
type BananaVariety =
  | Cavendish
  | GrosMichel
  | Manzano
  
type CherryVariety =
  | Montmorency
```

This can be read as:

* An `AppleVariety` is either a `GoldenDelicious` _OR_ a `GrannySmith` _OR_ a `Fuji`. 
* and so on for the other types of fruit.

Unlike the `FruitSnack` example, there is no extra data associated with each case -- they are just labels. 


### Simple types

We will often define a choice type with only *one* choice, such as this:

```
type EmailAddress =
  | EmailAddress of string
```  

This definition is generally simplified to one line, like this: 

```
type EmailAddress = EmailAddress of string
```

Why would we create such a type? Because it's an easy way to create a "wrapper" --  a type that contains a primitive (such as a `string` or `int`) as an inner value.

For example, we might define wrapper types like these:

```
type PersonalName = PersonalName of string
type EmailAddress = EmailAddress of string
type PhoneNumber = PhoneNumber of string
```

and having done this, we can be sure that these three types cannot be mixed up or confused. 

### Function types

Finally, there's one more kind of type to discuss: function types.
As we know from high school, a function is a kind of black box with an input and an output. Something goes in, is transformed somehow, and comes out the other side.

To describe a function abstractly, we just need to document the inputs and outputs.
So for example, to document a function that adds 1 to a value, we would say that it takes an `int` as input and returns an `int` as output. It would be documented like this:

```
type Add1 = int -> int
```

where the type of the input is listed first, followed by an arrow, and then the type of the output.

But of course the inputs and outputs can be any type, including domain-specific types. Which means that we can document a function that creates an `EmailAddress` domain object from a string like this:

```
type CreateEmailAddress = string -> EmailAddress
```

This can be read as: to use `CreateEmailAddress` you provide a `string` as input and then the output is an `EmailAddress`.

### Algebraic types = Composable types 

Now we can define what we mean by an algebraic type *system*.  It's not as scary as it sounds -- it's simply a type system where *every* compound type is composed from smaller types by *AND*-ing or *OR*-ing them together. Using _AND_ and _OR_ to build new data types should feel familiar -- we used the same kind of _AND_ and _OR_ to document our domain! 

This kind of *composable* type system is a great aid in doing domain-driven design because we can quickly create a complex model simply by mixing types together in different combinations, as we'll see next.


## Modeling with algebraic data types

Now we have everything we need to do some real modeling!
Let's revisit some of the domain descriptions at the top of this chapter, and model them using algebraic types.

### Modeling order lines

The description was: "An order line has an order id, a product id, and an order quantity."

We start by creating three distinct domain-specific types, and then define a record that ANDs them together:

```
type OrderId = OrderId of int
type ProductId = ProductId of int
type OrderQty = OrderQty of int

type OrderLine = {
  OrderId : OrderId
  ProductId : ProductId
  OrderQty : OrderQty
}
```

### Modeling contact information

The description was: "Contact information consists of a personal name and a contact method, where a contact method is either an email address or a phone number."

Again, we have three "primitive" domain types:

```
type PersonalName = PersonalName of string
type EmailAddress = EmailAddress of string
type PhoneNumber = PhoneNumber of string
```

And then we can define a choice type with `EmailAddress` and `PhoneNumber` as alternatives.

```
type ContactMethod = 
  | ByEmail of EmailAddress
  | ByPhone of PhoneNumber
```

Finally, we can combine the `PersonalName` and `ContactMethod` into a record:

```    
type ContactInformation = {
  Name : PersonalName
  ContactMethod : ContactMethod
}
```

### Modeling purchasers

The description was: "A purchaser is either a one-time 'guest' or has been registered on the website. A registered purchaser has been given a customer id, which a guest doesn't have."

We start by defining two distinct types, one for each case, plus a primitive `CustomerId` type:

```
type GuestPurchaser = {
  Name : PersonalName
  ContactMethod : ContactMethod
}

type CustomerId = CustomerId of int

type RegisteredPurchaser = {
  Id: CustomerId
  Name : PersonalName
  ContactMethod : ContactMethod
}
```

And we can then create a choice type with the alternatives:

```
type Purchaser = 
  | Guest of GuestPurchaser
  | Registered of RegisteredPurchaser
```


### Modeling email addresses

The description was: "An email is either validated or unvalidated. Password resets should only be sent to validated emails."

It's important to distinguish between `Unvalidated` and `Validated` emails -- there are a different business rules around them, so we should define distinct types for each of these, and a choice type to combine them:

```
type UnvalidatedEmailAddress = UnvalidatedEmailAddress of string
type ValidatedEmailAddress = ValidatedEmailAddress of string

type EmailAddress =
 | Unvalidated of UnvalidatedEmailAddress
 | Validated of ValidatedEmailAddress
```

We can document the password reset process like this:

```
type SendPasswordResetLink = 
  ResetLinkUrl -> ValidatedEmailAddress -> output???
```

We're not sure what the output is, so we'll just leave it undefined for now. Also, details of how the email gets sent (e.g. via a SMTP server) are not relevant to the domain model right now, so we will not document that here.

Finally, we can document the email validation process like this:

```
type ValidationToken = ValidationToken of string // some opaque token

type ValidateEmailAddress = 
  UnvalidatedEmailAddress -> ValidationToken -> ValidatedEmailAddress
```

### Documenting failures

But that's not quite right, because we said that the action might fail. There was a *choice* between two kinds of output, if successful a `ValidatedEmailAddress`,
but if there was an error, some sort of error message. We can handle this by creating *another* choice type to represent the result:

```
type ValidationResult = 
  | Ok of ValidatedEmailAddress
  | Error of string
```

and then we can use `ValidationResult` as the output of the validation process instead of `ValidatedEmailAddress`:

```
type ValidateEmailAddress = 
  UnvalidatedEmailAddress -> ValidationToken -> ValidationResult
```


If we wanted to be specific about the kinds of errors that could occur, we could document them with yet another choice type, say `ValidationError` and then use that type in the result:

```
type ValidationError =
  | WrongEmailAddress
  | TokenExpired
  
type ValidationResult = 
  | Ok of ValidatedEmailAddress
  | Error of ValidationError
```

This kind of "result" type is so common that it is available as a built-in generic type in most functional languages, defined like this:

```
type Result<'SuccessType,'FailureType> = 
  | Ok of 'SuccessType
  | Error of 'FailureType
```

Using this built-in type then, the function definition looks like this:

```
type ValidateEmailAddress = 
  UnvalidatedEmailAddress -> ValidationToken -> Result<ValidatedEmailAddress,ValidationError>
```

### Sketching a domain model by composing types

This kind of modeling is not a heavyweight "big design up front". Just the opposite. It's very useful for "design sketches", written in conjunction with a domain expert during a discussion.

For example, say that we want to track payments for an e-commerce site. Let's see how this might be sketched out in code during a design session.

First, we start with some wrappers for the primitive types, such as `CheckNumber`. These are the "primitive types" we discussed above. Doing this gives them meaningful names and makes the rest of the domain easier to understand.
 
```
type CheckNumber = CheckNumber of int
type CardNumber = CardNumber of string
``` 

Next, as we discuss credit cards further, we might build up some more low-level types. A `CardType` is an _OR_ type -- a choice between `Visa` *or* `Mastercard`, while `CreditCardInfo` is an _AND_ type, a record containing a `CardType` *and* a `CardNumber`:

```
type CardType =
  Visa | Mastercard // 'OR' type
  
type CreditCardInfo = { // 'AND' type (record)
  CardType : CardType
  CardNumber : CardNumber
}
```

We learn that the business will accept case, checks, or credit cards, so we then define another _OR_ type, `PaymentMethod`, as a choice between `Cash` or `Check` or `Card`. This is no longer a simple "enum" because some of the choices have data associated with them: the `Check` case has a `CheckNumber` and the `Card` case has `CreditCardInfo`:

```
type PaymentMethod =
  | Cash
  | Check of CheckNumber
  | Card of CreditCardInfo
```

Next we might talk about money, which leads us to define a few more types, such as `PaymentAmount` and `Currency`:

```
type PaymentAmount = PaymentAmount of decimal
type Currency = EUR | USD
```

And finally, the top-level type, `Payment`, is a record containing a `PaymentAmount` *and* a `Currency` *and* a `PaymentMethod`:

```
type Payment = {
  Amount : PaymentAmount
  Currency: Currency
  Method: PaymentMethod
}
```

So there you go. In about 25 lines of code, we have defined a pretty useful set of types already.

Of course, there is no behavior directly associated with these types because this is a functional model, not an object-oriented model.
To document the actions that can be taken, we instead define types that represent functions.

So, for example, if we want to show there is a way to use a `Payment` type to pay for an unpaid invoice, where the final result is a paid invoice, we could define a function type that looks like this:

```
type PayInvoice = UnpaidInvoice -> Payment -> PaidInvoice
```

Which means this: Given an `UnpaidInvoice` and then a `Payment`, we can create a `PaidInvoice`.

Or, to convert a payment from one currency to another:

```
type ConvertPaymentCurrency = Payment -> Currency -> Payment
```

where the first `Payment` is the input, the second parameter (`Currency`) is the currency to convert to, and the second `Payment` -- the output -- is the result after the conversion.

## Value Objects, Entities and Aggregates

We've now got a basic understanding of how to model the domain types and workflows, so let's move on and look at an important way of classifying data
types, based on whether they have a persistent identity or not. In DDD terminology, objects with a persistent identity are called *Entities* and
objects without a persistent identity are called *Value Objects*. 

### Value objects

In many cases, the data objects we are dealing with have no identity -- they are interchangeable. For example, one instance of a `CustomerId` with value
"1234" is the same as any other `CustomerId` with value "1234." We do not need to keep track of which one is which -- they are equal to each other.

When we model a domain using an algebraic type system, the types we create will implement this kind of field-based equality testing automatically! We
don't need to write any special equality code ourselves, which is nice.
To be precise, in an algebraic type system, two record values (of the same type) are equal if all their fields are equal, and two choice types are equal if they have the same choice
case, and the data associated with that case is also equal. This is called *Structural Equality*.

### Entities

However, we often model things that, in the real world, do have a unique identity, even as their components change. For example, even if I change my name or my address, I am still the same person. In DDD terminology, we call such things *Entities*.

In a business context, Entities are often a document of some kind: Orders, Quotes, Invoices, Customer profiles, product sheets, etc. They have a *lifecycle* and are transformed from one state to another by various business processes. 

Entities need to have a stable identity despite any changes, and therefore, when modeling them, we need to give them a unique identifier or key, such as an "Order Id," or "Customer Id." For example, the `UnpaidInvoice` type below has an `InvoiceId` that stays the same even if the `AmountDue` changes.

```
type UnpaidInvoice = {
  Id: InvoiceId
  AmountDue : InvoiceAmount
}
```

And of course, when we model different states in a lifecycle with distinct types, we must ensure that all the states have a common identifier field.
The `PaidInvoice` type below, also has an `InvoiceId` field:

```
type PaidInvoice = {
  Id: InvoiceId
  AmountPaid : InvoiceAmount
  PaymentDetails :  PaymentDetails
}
```

We saw earlier that, by default, equality in an algebraic type system uses all the fields of a record. But when we compare Entities we want to use only one field, the
identifier. That means, in order to model Entities correctly, we must change the default behavior.

One way of doing this is to create a custom equality test so that only the identifier is used, but that can be error prone in some cases. 
Therefore, a sometimes preferable alternative is to disallow equality testing on the object altogether!

In F# this can be done by adding a `NoEquality` type annotation like this:

```
[<NoEquality; NoComparison>]
type UnpaidInvoice = {
  Id: InvoiceId
  AmountDue : InvoiceAmount
}
```

Now when we attempt to compare values with this annotation, we get a compiler error. Of course we can still compare the `InvoiceId` fields directly.
The benefit of the "NoEquality" approach is that it removes any ambiguity about what equality means for a particular type, and forces us to be explicit.

## Immutability as a design aid

In functional programming languages, algebraic data types are immutable by default, which means that none of the objects defined so far can be changed after being initialized.

How does this affect our design?

* For *Value Objects*, immutability is required. Think of how we use them in common speech: if we change any part of a personal name, say, we call it a *new*, distinct name, not the same name with different data. The fact that immutability is the default means that Value Objects are very easy to implement.
* For *Entities*, it's a different matter. We expect the data associated with Entities to change over time; that's the whole point of having a constant identifier. So how can immutable data structures be made to work this way? The answer is that we make a *copy* of the Entity with the changed data while preserving the identity.
All this copying seems like it might be a lot of extra work but isn't an issue in practice. Functional programming languages have built in support to make this easy.

A benefit of using immutable data structures is that any changes have to be made *explicit* in the type signature. For example, if we want to write a function that changes the `AmountDue` field in a `UnpaidInvoice`, we can't use a function with a signature like this (where `unit` means no output):

```
type UpdateAmountDue = UnpaidInvoice -> AmountDue -> unit
```

That function has no output, which implies that nothing changed! Instead, our function must have a `UnpaidInvoice` type as the output as well, like this:

```
type UpdateAmountDue = UnpaidInvoice -> AmountDue -> UnpaidInvoice
```

This clearly indicates that, given a `UnpaidInvoice` and a `AmountDue`, a different `UnpaidInvoice` is being returned. Immutability has forced us to make the logic explicit in the design.

### Immutability and aggregate boundaries

Immutability can be particularly helpful for determining aggregate boundaries.
Say that we have an `Order` which contains a list of lines of type `OrderLine`:

```
type OrderLine = {
  OrderLineId : OrderLineId
  ProductId : ProductId
  OrderQty : OrderQty
}

type Order = {
  OrderId : OrderId
  Lines : OrderLine list
}
```

But now here's a question: if you change an `OrderLine`, have you also changed the `Order` that it belongs to?
In this case, it's clear that the answer is yes: changing a line also changes the entire order.

With immutable data. this design is unavoidable. If I have an immutable `Order` containing immutable `OrderLines`, then just making a copy of one of the order lines *does not* also make a copy of the `Order` as well. In order to make a change to an `OrderLine` contained in an `Order`, I need to make the change at the level of the `Order`, not at the level of the `OrderLine`.

For example, here's the definition of a function that updates the price of a specific order line. We need an `Order`, the `OrderLineId` of the line to change, and the new `Price`:

```
type ChangeOrderLinePrice = Order -> OrderLineId -> Price -> Order 
```

The final result, the output of the function, is a new `Order` containing a new list of lines, where one of the lines has a new price.
You can see that immutability causes a ripple effect in a data structure, whereby changing one low-level component can force changes to higher-level components too.

Therefore, even though we're just changing one of its "subentities" (an `OrderLine`), we *always* have to work at the level of the `Order` itself.
In other words, immutability has forced us to define the aggregate root to be the `Order`, and requires us to make all changes at this level rather than at the order line level, which is just what we want.

### Aggregate references

Now let's say that we need information about a customer to be associated with an `Order`. A bad design might be to add the `Customer` as a field of an `Order`, like this:

```
type Order = {
  OrderId : OrderId
  Customer : Customer // info about associated customer
  Lines : OrderLine list
  // etc
  }
```

How can we tell that this is a bad design? The ripple effect of immutability forces us to say that if I change any part of the *customer*, I must also change the *order* as well. Is that really what we want?

No, probably not. It's clear that a better design would be to store a *reference* to the customer, not the whole customer record itself. That is, we would just store a `CustomerId` in the `Order` type, like this:

```
type Order = {
  OrderId : OrderId
  CustomerId : CustomerId // reference to associated customer
  Lines : OrderLine list
  // etc
}
```

Then when we need the full information about the customer, we would get the `CustomerId` from the `Order` and then load the relevant customer data from the database separately, rather than loading it as part of the order. In other words, the `Customer` and the `Order` are *distinct* and *independent* aggregates. They each are responsible for their own internal consistency, and the only connection between them is via the identifiers of their root objects.

Again, we can see that immutability has been used as a design aid to define whether entities are in the same aggregate (orders and order lines) or are separate (orders and customers).

## Making illegal states unrepresentable

Since we've gone to this trouble to model the domain properly, we should take some precautions to make sure that any data in this domain is valid and consistent. The goal is to create a bounded context that always contains data we can trust, as distinct from the untrusted outside world. If we can be sure that all data is always valid, the implementation can stay clean and we can avoid having to do defensive coding.

So, in this final section, we'll look at some techniques to avoid invalid data by making illegal states unrepresentable.
That is, the rules and logic are made explicit in the *design itself*, rather than relying on methods buried in the code somewhere.
Furthermore, in a type-checked language, the data cannot become invalid because the compiler will not allow it! This means that fewer unit tests are needed, less defensive code, and less implementation effort in general.

Here as some common things that we can do in the design:

* Avoid nulls with optional values
* Enforce constraints
* Enforce business rules

### Avoiding nulls with optional values

Nulls have been the bane of programmers for 50 years. Their own creator called them a "billion dollar mistake". From a design point of view, they complicate matters because we can never be sure whether a value is meant to be optional or not.

In most languages with algebraic type systems, nulls do not exist. That means that every time we reference a value in a domain model, it's a *required* value.

But of course we *do* sometimes need to indicate that data might be optional in certain cases. How can we represent that in the design?
 
The answer is to think about what missing data means: it's either present or absent. There's something there, or nothing there.
We can model this with a choice type called `Option` in F# (and `Maybe` in other languages), defined like this:

```
type Option<'a> =
  | Some of 'a
  | None
```

The `Some` case means that there is data stored in the associated value `'a`. The `None` case means there is no data.
The tick in `'a` is F#'s way of indicating a generic type --  that is, the `Option` type can be used to wrap *any* other type.
The C# or Java equivalent would be something like `Option<T>`.

To indicate optional data in the domain model then, we wrap the type in `Option<..>` just as we would in C# or Java. For example, if we have a `PersonalName`
type and the first and last names are required, but the middle initial was optional, we could model it like this:

```
type PersonalName = {
  FirstName : string            // required
  MiddleInitial: Option<string> // optional
  LastName : string             // required
}
```

### Enforcing constraints

It is very rare to have a unbounded integer or string in a real-world domain. Almost always, these values are constrained in some way.
In the earlier examples we mentioned some values like this:

```
data OrderQuantity is int // constrained to be between 1 and 100
data EmailAddress is string // Must not be null or empty. Must contain @ symbol.
```

Rather than allowing the raw `int` and `string` values to be used, we want to ensure that, if we *do* have a `OrderQuantity` or `EmailAddress`, then
we know that the constraints have been satisfied. If we never need to check them, then that eliminates yet more defensive coding.


Sounds great, so how do we ensure that the constraints are enforced? The answer: the same way as we would in any programming language -- make the constructor private and have a separate function that creates valid values and rejects invalid values, returning an error instead. In FP communities, this is sometimes called the *smart constructor* approach.

Here's an example of this approach applied to OrderQuantity:

```
type OrderQuantity = private OrderQuantity of int
                  // ^ private constructor
                  
// define a module with the same name as the type
module OrderQuantity =

  /// Define a "smart constructor" for OrderQuantity
  /// int -> Result<OrderQuantity,string>
  let create qty =
    if qty < 1 then
      // failure
      Error "OrderQuantity can not be negative"
    else if qty > 100 then
      // failure
      Error "OrderQuantity can not be more than 100"
    else
      // success -- construct the return value
      Ok (OrderQuantity qty)
                  
```

So now an `OrderQuantity` value can *not* be created directly, due to the private constructor. But it *can* be created using the "factory" function `OrderQuantity.create`.

The `create` function accepts an `int` and returns a `Result` type to return a success or failure. These two possibilities are made explicit in its function signature:

```
int -> Result<OrderQuantity,string>.
```

The design tells us straight away that creating an `OrderQuantity` might fail.
But, once created, immutability ensures that an `OrderQuantity` will never change and thus always be valid thereafter.


### Capturing business rules in the design

Can we document business rules using just the type system? That is, we'd like to use the type system to represent what is valid or invalid so that the compiler can check it for us, instead of relying on runtime checks or code comments to ensure the rules are maintained.

Let's say we have a business rule around contacting a customer: "A customer must have an email or a postal address."

How should we represent this? The obvious approach is just to create a record with both an `Email` and an `Address` property, like this:

```
type Contact = {
  Name: Name
  Email: EmailContactInfo
  Address: PostalContactInfo
}
```

But this is an incorrect design. It implies both `Email` and `Address` are required. 

OK, so let's make them optional:

```
type Contact = {
  Name: Name
  Email: EmailContactInfo option
  Address: PostalContactInfo option
}
```

But this is not correct either. As it stands, `Email` and `Address` could both be missing, and that would break the business rule.

Now, of course, we could add special runtime validation checks to make sure that this couldn't happen. But can we do better and represent this in the type
system? Yes, we can!

The trick is to look at the rule closely. It implies that a customer:

* Has an email address only, or
* Has a postal address only, or
* Has both an email address and a postal address.

That's only *three* possibilities. And how can we represent these three possibilities? With a choice type of course!

```
type BothContactMethods = {
  Email: EmailContactInfo
  Address : PostalContactInfo
}

type ContactInfo =
  | EmailOnly of EmailContactInfo
  | AddrOnly of PostalContactInfo
  | EmailAndAddr of BothContactMethods
```  
  
And then we can use this choice type in the main `Contact` type, like this:

```
type Contact = {
  Name: Name
  ContactInfo : ContactInfo
}
```

Again what we've done is good for developers (we can't accidentally have no contact information – one less test to write) but also it is good for the *design*.
The design makes it very clear that there are only three possible cases, and exactly what those three cases are. We don't need to look at documentation, we can just look at the code itself.


## Conclusion

If we look at some of the examples above, we should be happy. We have managed to capture the essence of the verbal domain descriptions, but as code rather than as text or documentation.

From a developer's point of view, we have attained one of the goals of Domain Driven Design -- compilable code that defines and implements the domain model and ubiquitous language. Another developer joining the project would be able to understand the domain model without having to translate between the implementation concepts and the domain concepts.

Furthermore, this code is still quite comprehensible for non-developers. What would a domain expert have to learn in order to understand this code as documentation? It certainly is more readable than a conventional programming language such as C# or Java.

This approach, using types as documentation, is very general and it should be clear how you can apply it to almost any domain modeling situation. Because there's no
implementation at this point, it's a great way to try ideas out quickly when you are collaborating with domain experts. And of course, because it is just
text, a domain expert can review it easily without needing special tools, and maybe even write some types themselves!
