# On objects, processes and data
#### From here to there and back again, Bilbo Baggins
## Introduction
Fifteen years has passed since Eric Evans seminal book Domain Driven Design was published. Since then a lot has happened. Back then there was no iPhone, no Facebook, no Netflix and Amazon had run with profitt for two years. Windows 2000 was Microsofts flagship operating system, Sun Microsystems was a leading tech company, Java was 9 years old and the relational database ruled as the enterprise data store.

Developers could be found arguing over Java vs  C# and applications was still made in tools like Microsoft Access. Martin Fowlers Patterns of Enterprise Application Architecture was less than a year old and the GoF Design Patterns, Elements of reusable object-oriented software had just turned 9.

Since then, cloud computing, big-data, mobile-apps, internet of things, edge analytics and machine learning has become part of our professional vocabulary. New programming languages such as Swift, Scala and Go has entered the scene and old languages such as Python have resurrected to dominates data science. 

The effects of all this is that computing itself has changed. Despite these changes, the principles and patterns of Domain Driven Design are still relevant and in many ways even more so as business capabilities are built on data with software.

While the needs in many ways are the same, the technology has enabled new oportunities that will demand more from the developers than before. There are more devices to manage, multi-core processors in smart phones require understanding and mastery of concurrency, the SQL database is replaced by a multitude of storate oportunities and so on. 

So, for domain driven design to stay relevant and still be a driving force it need to embrace the new reality that surrounds us. With that I would like to say welcome to what I like to call Domain-Driven Design 4.0. 

Domain-Driven Design sprang out of Eric's experience developing business systems using object oriented languages during the late 1990ties. His experience was that developers and domain experts needed a common language to succeed, and that developers very often fell in love with the  technology, loosing out on the inherent complexity found in the domain at hand. The result was poor software quality, software that lacked the conceptual integrity required by a quality products.

Success was most often found in projects where the team had invested time digging into the domain and implemented the core domain concepts the products code base. The crux was to establish a common language that supported the communication between developers and domain experts. The developers stopped talking about database tables and rows and began talking about transfers of money, settlement of orders and cargo lifiting.

Another aspect was the architectural and technological landscape at the time. The PC had favoured a software architecture where a fat or rich clients accessed data stored in a relational database. Data gravity ensured that applications that started out small grew until the entropy got out of hand. It was always easier to add a new table than starting from scratch. Retrofitting old applications to work on the web using frameworks such as Enterprise Java din not help. In many ways they made things worse, moving focus away from the domain and to the technology.  

The programming styles emerging from the rich Windows clients propagated to the server side, following what Martin Fowler so brilliantly called the transactional script. These are GUI event handlers that tries to bring the effect of a mouse click to the database. To boost performance, critical business logic was moved from the client to the database using stored procedures maintaining the same programming style. I personally know systems where the database contain more than 1.5 million lines of PLSQL and have stored procedures more than 10.000 lines long.

Domain-Driven Design was born at a point in time where there was a strong belief in that object oriented programming thee mean to reduce complexity and boost developer productivity. The result we know, the ubiquitous language, context maps, core domain, supporting domain, entities, value objects, repositories, domain service, repository, factory, aggregates are all good helpers for those who was willing to invest in domain modelling and to bring the domain model into the code. 

# Domain-Driven Design 4.0
Computing has experienced a profound change over the last 15 years, and there are at least three concerns that would benefit from beeing addressed in context of Domain-Driven Design.

Firstly, the cloud enables us to separate data from application, and to free us from the relational data model was the only storage model of business data. It s now possible to store data in fit for purpose data stores, it be graphs, key-value, relational or lake, and by doing so we are able to reduce the data gravity cost. This change will have a huge impact on how we address entities, value objects, repositories and aggregates. We can call this the data separation pattern or the master data repository.

Secondly, the real world consist of dynamic systems. Object oriented programming itself was created for the purpose of analysis of such systems. Business software developers has historically been spared from the challenges that comes with real-time dynamic systems, that was the realm of the system programmers. The Internet of Things changes this. Back-office processes must be able to respond to events at the edge, and they must be able to send new instructions to the edge process and devices. Architecturally this is solved using publish-subscribe and event processing. We can call the pattern concurrent and asynchronous processes.

Thirdly, new modern programming languages such as Swift unites object oriented programming and functional programming in ways that both supports and simplifies DDD. Remember, objects has state and functions are stateless. These properties become crucial when we are aiming at implementations of master data repository and concurrent asynchronous processes in a distributed environment. We need to implement rich domain models at both the edge and in the cloud.
 
With the scene set, let's roll.

## Separating data from the applications
Master data is defined as the business objects that contain the most valuable, agreed upon information that is shared across a business. The master data objects are the bearers of identity and lineage. In Domain-Driven Design is it the Entities that has this responsibility. Working with entities or master data objects implies working with who they are, more than what they are and maintaining their identity and lineage accross different bounded contexts.

The biggest difference between an Entity and a master data object is that when we work with an Entity our primary concerns are the Entities role in a specific bounded context, while a master data object involves maintaining identity and lineage accross multiple bounded contexts.

In the upstream oil and gas "Well" is one of the core master data objects with a lifespan measured in decades. Well data is typically scattered over multiple data stores, each store using its own conventions, standards and codings. Seen from the enterprise level, lineage and identity is easily broken and keeping it intact is very expensive. In healtcare Patient is a master data object and the same can be said about Item in retail.

Based on work we have done in collaboration with other oil companies we discovered that the best way forward was to separate lifecycle management of master data objects from the applications. We have called this the application data separation pattern.

It can be implemented by creating a master data repository that provide a context independent home for the master data objects, maintaining lineage (immutability and versioning) and holding references to attributes, life-events and decisions. This mean that management of identity and lineage is moved out of the applications and to the repository, simplifying the concerns at the application level.

The master data repository API provide services for Ingestion, Search and Delivery. The internal representation of the repository matches best with a graph, where the objects life events are tracked and versioned accordingly with reference to where member data is stored. The master data repository ingestion and delivery service operates with aggregates. An aggregate understood as a clusters of entities and value objects with consistent boundaries that are managed as a whole.

On the client side, this makes a lot of things easier. The consuming contexts can focus on the processes, the workflows and the dynamic properties of the domain working with entities and value objects without being bothered with identity and lineage except as how these concerns materialises in the API. 
 
## Processes, events and tasks
The real world consists of asynchronous, concurrent and dynamic processes, sometimes competing other times collaborating. Object oriented programming was created to study and analyse such processes in context of a system. A system being a part of the world that is regarded as a whole, with its interacting components (objects).

We choose to call these objects or functions who's role it is to perform work for process controllers. A process controller will process events in line with its internal state, update its internal state and execute tasks. What task to choose as respons to an event is state dependent. Process controller state might be persisted, and the controllers themselves might be managed as entities. Process controllers might often be the home for a domain service. 

By maiking dynamic domain modelling explicit we end up with four new concepts:
- Domain processes and process controllers are designated objects that represents a larger piece of work. It might provide domain services, but are more often associated with events processing and execution of tasks.
- Domain events capturing the occurrences of something that happens in the domain (Vernon).
- Domain tasks capturing the work to be performed by the process controller as response to a domain event.
- Domain state capturing the state guiding the process controllers selection of task on events.

These building blocks are similar to what we find in the multi-agent design paradigme. 

The internal model of an object that processes events and performs task can be rather complicated. Think of the model in a  smart phone application following the model-view-controller pattern. It will most likely consists of multiple modules (packages) and depend on external libraries.

To support the design and implementations of these workhorses of your domain the GoF book provide several useful patterns such as: Chain of responsibility, Command, Observer and State. To study these patterns and others is highly recommended. For those who want to take it one step further "Doing hard time" (Douglas) is a good read.

Lastly, process controllers can be implemented in many ways. It can be the model in a iPhone application using grand dispatch, a Java Servlet, a Java thread, an Ada task or as a Unix cron job.

## Object-Funcinal languages
Since 2003 several new modern programming languages that supports both object oriented and functional programming has emerged. One of these languages is Swift, others are Scala and Go. I will use Swift as the basis. In functional languages functions are first class citizens. Being a first class citizen enables the developers to use functions and methods like any other object or value. Functions can be passed as values, stored in properties and be returned as output from another functions.

Swift make a clear distinction between reference types (class) and value types (enumerations, structs and tuples). Objects created as a reference type share a copy of the same instance.

class A { }

var a: A()

var b : A = a

Here both an and b refer to the same instance of A. The effect is that a change to variable a will impact variable b and vice versa.

Value types keeps a unique copy of its data.

struct B {}

var b: B()

var c : B = b

In this case variable c is made a copy of b and they can be independently changed.

With functions as first class citizens we can create structures like this:

typealias Output = (Int) -> Int

typealias Input = (Int, String, float) -> Bool

func doSomething(Input) -> (SomeType) { }

A final property with functions is that they fit very well with multicore architectures, as we can execute them in their own threads in a safe way. Swift provides as an example a library called the Grand Dispatch that make concurrent programming using mulicore's a simpler feat than raw threads programming has proved to be.

Entities are defined as objects known defined by their identity and their lineage. They are most often best implemented as a reference type (class). Their identity should come from their standing in the business, and they should just conform to a protocol as illustrated below.

struct Identity {}

Protocol Entity {

	func ==(Entity) -> Bool
	
}

class Well: Identity {

	func  ==(Entity) -> Bool { .. }

}

Value objects on the other hand are just values, and can be implemented using class, struct, enumeration, tuple and function. This mean that we have a much richer toolkit when designing them than we had back in 2003 and its something we need to dig into and develop good design practices for.

Well designed software is characterised by a few very recognisable properties and with languages where functions and objects are both first class citizens, it become important to map the characteristics of good software to the new language paradigm:

- Modularity: In stead of thinking of a program as a sequence of assignments and method calls (imperative style), functional programmers emphasise that each program can be repeatably broken into smaller and smaller pieces that can be assembled using function applications to define the complete program. This only works if we can avoid sharing state between the individual components, that takes us to the next point.

- Managing mutable state: While object oriented programming focuses on the design of objects, each with their own encapsulated state functional programming emphasises programming  with values, free of mutable state and other side effects. By avoiding mutable state, functional programs can be much more easily combined than their object oriented siblings.

- Types: A well designed functional program makes careful use of types. More than any programming concepts, such as class, methods and variables.

With a richer toolkit we need to learn how to embrace and use the toolkit to build better software, and to make the richer toolkit part of Domain-Driven Design.

# Conclusion
I have tried to illustrate some of the bigger changes that have taken place since Eric's seminal book came into being 15 years ago, and I have tried to put forward arguments for new strategic patterns (master data repository), direct support for dynamic domains where the core is the processes, not the data and finally illustrate that new programming languages such as Swift that unites object oriented and functional programming paradigms create a new opportunity space for architects and programmers alike.


# References
GoF, Design patterns, Elements of reusable object oriented software.

Fowler, Patterns of Enterprise Applications

Douglas, Doing hard time, Developing real-time systems with UML, Objects, Frameworks and Patterns

Evans, Domain-Driven Design

Vernon, Implementing Domain Drive Design

Eidhof et al, Functional Swift


