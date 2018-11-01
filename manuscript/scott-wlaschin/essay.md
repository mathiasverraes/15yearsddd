# Domain Modeling with Algebraic Data Types (by Scott Wlaschin)

One of the main goals of Domain Driven Design is to encourage good communication between the development team, domain experts, and other stakeholders.
In particular, there should be a very close correspondence between the mental model of the domain experts and the code used in the implementation.

Traditionally, Domain Driven Design has been done using object-oriented techniques. In this chapter, I'd like to show that a domain model built using algebraic data types (commonly used in functional programming) is a alternative approach with great potential.

## Discovering common concepts in domain modeling

When we talk to domain experts during a discovery phase, we will typically have descriptions of the domain like this:

* "An order line has an order id, a product id, and an order quantity".
* "Contact information consists of a personal name and a contact method, where a contact method is either an email address or a phone number".
* "An email is either validated or unvalidated. Password resets should only be sent to validated emails."
* "A purchaser is either a one-time 'guest' or has been registered on the website. A registered purchaser has been given a customer id, which a guest doesn't have."
* "To pay for an invoice, you start with an unpaid invoice and payment information, and you end up with a paid invoice."

As we build our Ubiquitous Language from these discussions, there are some common groupings that we can use. They are:

* Primitive values
* Groups of things treated as one 
* Choices between things (values are 'or'ed together)
* Actions and workflows
* States and lifecycles

Let's look at each of these in more detail.

### Primitive Values

Domain experts will never talk about "integers" or "strings". Instead, they will use domain concepts like "order quantity" or "email address".

These concepts may be *represented* by an integer or string, but they are not equivalent. 

For example, an "order id", a "product id", and an "order quantity" may all be represented by integers, but the domain concepts are in no way equivalent to an integer.
It doesn't make sense to multiply a product id by two, for example. 

And even concepts which are integers don't correspond to a programmers `int` -- there are almost always constraints. For example, an "order quantity" must be one or more,
and probably has an upper bound as well, such as 100. It's unlikely that a sales system would let you order 2 billion items!

Similarly an "email address" and a "phone number" might both be represented by strings, but again they are not interchangable, and each will have special constraints.

If we were to document some of these primitive values, we might make notes like this:

```
data OrderId              // opaque -- don't care about representation
data ProductId            // opaque -- don't care about representation
data OrderQuantity of int // constrained to be between 1 and 100

data PersonalName of string // Must not be null or empty. Must be less than 100 characters.
data EmailAddress of string // Must not be null or empty. Must contain @ symbol.
data PhoneNumber of string  // Must not be null or empty. Must only contain digits, parens or hyphen.
```

When we come to translate these notes into code, we will want to preserve the simplicity of these notes.
The code should represent the domain as closely as possible.

### Groups of Things Treated as One Thing

Of course, some domain values are not primitive, but are composed of other smaller values.

To document these kinds of things, we might make notes using AND to group the values together, like this:

```
data OrderLine = OrderId AND ProductId AND OrderQuantity
data ContactInformation = PersonalName AND ContactMethod
```

## Choices Between Things

Another common pattern is that a concept is comprised of alternatives.

* "An email is either validated or unvalidated"
* "A purchaser is either a one-time 'guest' or a registered customer"
* "An invoice is unpaid or paid"

For these cases, we could use OR in our notes, like this:

```
data Email = UnvalidatedEmail OR ValidatedEmail
data ContactMethod = EmailAddress OR PhoneNumber
data Purchaser = GuestPurchaser OR RegisteredPurchaser (contains CustomerId)
data Invoice = UnpaidInvoice OR PaidInvoice
```

It's important to realize that these alternatives generally play a critical role in business rules. For example:

* A password reset link should only be sent to a `ValidatedEmail`.
* Discounts should only be given to a `RegisteredPurchaser`.
* You can only apply a payment to an `UnpaidInvoice`.

Failing to clearly distinguish between these kinds of choices results in at best, a confusing design, and at worse, seriously defective implementations.

### Fighting the Impulse to Do Class-Driven Design

One of the key tenets of Domain Driven Design is *persistence ignorance*. It is an important principle because it forces you to focus on modeling the domain accurately, without worrying about the representation of the data in a database.

Indeed, if you're an experienced object-oriented developer, then the idea of not being biased to a particular database model will be familiar, Object-oriented techniques such as dependency injection encourage you to separate the database implementation from the business logic.

But we also have to be careful of introducing bias into the design if we think in terms of objects and classes rather than the domain.

For example, as the domain expert talks about different kinds of contact methods, you may be tempted to create a class hierarchy in your head, like this:

```
class ContactMethodBase ...
class EmailAddressContactMethod extends ContactMethodBase ...
class PhoneNumberContactMethod extends ContactMethodBase ...
```

Letting classes drive the design can be just as dangerous as letting a database drive the design -- again, we're not really listening to the requirements!

For example, in our class hierarchy we have introduced an artificial base class, `ContactMethodBase`, that doesn't exist in the real world. This is a distortion of the domain. Try asking the domain expert what an `ContactMethodBase` is! 

Similarly, an `EmailAddress` is a reusable primitive value, not specific to contact methods, so to use it in this particular context we have had to create a
wrapper class `EmailAddressContactMethod`. Again, this is another artificial object in the code that does not represent something in the domain.

The lesson here is that we should keep our minds open during requirements gathering and not impose our own technical ideas on the domain.


### Actions and workflows

So far, we've been talking about "nouns" in our domain -- the data. But of course static data -- data that is just sitting there unused -- is not contributing anything. 

So what causes an employee (or automated process) to start working with that data and adding value?
Often it's an outside trigger (a piece of mail arriving or your phone ringing), but it can also be a time-based trigger (you do something every day at 10 a.m.) or an observation (there are no more orders in the inbox to process, so do something else).

Whatever it is, it's important to capture it as part of the design. We generally call these things *Domain Events*. 

Domain Events are the starting point for almost all of the business processes we want to model.

For example:

* "payment received" is a Domain Event that will kick off the "applying payment" workflow
* "email validation link clicked" is a Domain Event that will kick off the "validate email" workflow

To document these workflows, we need to describe what the inputs and outputs are:

```
workflow ApplyPaymentToInvoice =  
   inputs: UnpaidInvoice, Payment
   outputs: PaidInvoice    
   
workflow ValidateEmail  =
   inputs: UnvalidatedEmail, ValidationToken (from clicked link)
   outputs: ValidatedEmail OR error
```

In the second case, the validation might fail (e.g. the link has expired) and so the output is written as *choice* between alternatives: a validated email address, or an error.


### States and lifecycles

Most important business entities have a lifecycle -- they go through a series of changes over time. 

* An invoice starts off as unpaid, and then transitions to being paid.
* A customer starts off as being a guest, and then transitions to being registered.

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

## Understanding Algebraic Data Types

So far, we've looked at some common concepts in the domain modeling, but we have not yet discussed how they can be mapped into code.

In this section, we'll define *Algebraic Data Types* and then in the next section, we'll see how they can be used to capture our domain model in a simple and explicit way.

### What are Algebraic Data Types?

In an algebraic type system, as used in many functional languages, new types are composed from smaller types in two ways:

* By _AND_ing them together
* By _OR_ing them together


### "AND" Types

Let's start with building types using _AND_.

For example, we might say that to make fruit salad you need an apple _and_ a banana _and_ some cherries:

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
The `Apple` value must be of type `AppleVariety`, the `Banana` value must be of type `BananaVariety`, and so on.


### "OR" Types

The other way of building new types is by using _OR_. 

For example, we might say that for a fruit snack you need an apple _or_ a banana _or_ some cherries:

Here's the definition of a `FruitSnack` using a choice type in F#:

```
type FruitSnack =
  | Apple of AppleVariety
  | Banana of BananaVariety
  | Cherries of CherryVariety
```

A choice type like this is also called a *sum type*. It can be read like this:

* A `FruitSnack` is either an `AppleVariety` (tagged with `Apple`) _or_ a `BananaVariety` (tagged with `Banana`) _or_ a `CherryVariety` (tagged with `Cherries`).

The vertical bar separates each choice, and the tags (such as `Apple` and `Banana`) are needed because sometimes the two or more choices may have the same type and so tags are needed to distinguish them. 

The varieties of fruit are themselves defined as _OR_ types, which in this case is used similarly to an `enum` in other languages.

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

* An `AppleVariety` is either a `GoldenDelicious` _or_ a `GrannySmith` _or_ a `Fuji`,

and so on.

### Simple Types

We will often define a choice type with only *one* choice, such as this:

```
type EmailAddress =
  | EmailAddress of string
```  

This type is almost always simplified to this: 

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


### Algebraic Type Systems

Now we can define what we mean by an "algebraic type system."  It's not as scary as it sounds -- an algebraic type system is simply one where every compound type is composed from smaller types by *AND*-ing or *OR*-ing them together. 

Using _AND_ and _OR_ to build new data types should feel familiar -- we used the same kind of _AND_ and _OR_ to document our domain! We'll see shortly that an algebraic type system is indeed an excellent tool for domain modeling.


### Function types

Finally, there's one more kind of type to discuss: function types.
As we know from high school, a function is a kind of black box with an input and an output. Something goes in, is transformed somehow, and comes out the other side.

To describe a function abstractly, we just need to document the inputs and outputs.
So for example, to document the `add1` function, we say that it takes an `int` as input and returns a `int` as output. It would be documented like this:

```
type Add1 = int -> int
```

where the type of the input is followed by an arrow, and then the type of the output.

But of course the inputs and outputs can be any type, including domain-specific types. For example, we can document a function that creates an email from a string like this:

```
type CreateEmailAddress = string -> EmailAddress
```

This can be read as: to `CreateEmailAddress` you need a `string` and then the output is an `EmailAddress`.

## Modeling with Algebraic Data Types

Now we have everything we need to do some real coding!
Now let's revisit some of the domain descriptions at the top of this chapter, and model them using algebraic types.

### Modeling Order Lines

The description was:

* "An order line has an order id, a product id, and an order quantity"

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

### Modeling Contact Information

The description was:

* "Contact information consists of a personal name and a contact method, where a contact method is either an email address or a phone number"

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

### Modeling Purchasers

The description was:

* "A purchaser is either a one-time 'guest' or has been registered on the website. A registered purchaser has been given a customer id, which a guest doesn't have."

We start by defining two distinct types: one for each case:

```
type CustomerId = CustomerId of int
type RegisteredPurchaser = {
  Id: CustomerId
  Name : PersonalName
  ContactMethod : ContactMethod
}

type GuestPurchaser = {
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


### Modeling Email Addresses

The description was:

* "An email is either validated or unvalidated. Password resets should only be sent to validated emails."

Again, we define types for each case, and a choice type:

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
  Url -> ValidatedEmailAddress -> ...
```

We're not sure what the output is, so we'll just leave it undefined for now.

Finally, we can document the validation process like this:

```
type ValidationToken = ValidationToken of string // some opaque token

type ValidateEmailAddress = 
  UnvalidatedEmailAddress -> ValidationToken -> ValidatedEmailAddress
```

### Documenting Failures

But that's not quite right, because we said that the action might fail. There was a *choice* between two kinds of output, if successful a `ValidatedEmailAddress`,
but if there was an error, some sort of error message. We can handle this by creating *another* choice type to represent the result:

```
type ValidationResult = 
  | Success of ValidatedEmailAddress
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
  | Success of ValidatedEmailAddress
  | Error of ValidationError
```

### Reviewing the Code as Domain Model

If we look at the domain model listed above, we should be pleased. We have a complete domain model, documented as F# types rather than as text,
but the types that we have designed look almost identical to the domain descriptions that we developed earlier using AND and OR notation.

From a developer's point of view, we have gained one of the key benefits of Domain Driven Design -- compilable code that defines and implements the domain model and ubiquitous language. Another developer joining the project would be able to understand the domain model without having to translate between the implementation concepts and the domain concepts.

Furthermore, this code is still quite comprehensible for non-developers. What would you have to learn in order to understand this code as documentation? You'd have to understand a little bit of syntax and might need some hand holding. It certainly is more readable than a conventional programming language such as C# or Java.

This approach, using types as documentation, is very general and it should be clear how you can apply it to almost any domain modeling situation. Because there’s no
implementation at this point, it's a great way to try ideas out quickly when you are collaborating with domain experts. And of course, because it is just
text, a domain expert can review it easily without needing special tools, and maybe even write some types themselves!


## Enhancing the model

There are a few aspects of the design that we haven’t yet addressed though. 

* **Value Objects, Entities and Aggregates.** How do these Domain Driven Design concepts work with our type centric domain modeling approach?
* **Constraints.** We said that an `OrderQty` must be between 1 and 100. How do we ensure that types like this are always constrained correctly? 
* **Business Rules.** How can we ensure that emails are validated properly before sending a password reset? What's to stop someone accidentally creating a `ValidatedEmailAddress` that hasn't actually been validated?

TO DO
