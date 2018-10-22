# On objects, processes and data
#### From here to there and back again, Bilbo Baggins (Lord of the Rings)
## Introduction
Fifteen years has passed since Eric Evans seminal book Domain Driven Design was published. Back then, there was no iPhone, no Facebook, no Netflix and Amazon had been profitable for two years. Windows 2000 was Microsofts flagship operating system, Sun Microsystems was a leading tech company, Java was 9 years old and the relational database ruled the enterprise data centers.

Developers could be found arguing over Java vs  C# and applications was still made in tools like Microsoft Access. Martin Fowlers Patterns of Enterprise Application Architecture was less than a year old and the GoF Design Patterns, Elements of reusable object-oriented software had just turned 9.

Since then, cloud computing, big-data, mobile-apps, internet of things, edge analytics, machine learning and artificial intelligence has become part of our professions vocabulary. New programming languages such as Swift, Scala and Go has entered the scene and old languages such as Python have resurrected to dominates data science. 

It is easy to argue that our profession is profoundly changed. Despite these changes, the principles and patterns of Domain Driven Design are still relevant and in many ways even more so as industry and society is digitalized and new business capabilities and models are built with software.

Technology has created new, oportunities, oportunities that demand more from the developers than before. There are more devices to manage, multi-core processors in smart phones require skills in concurrent programming, the SQL database is replaced by a multitude of storate oportunities. Open source software is embraced and is found everywhere. 

My claim is that shall Domain-Driven Design prosper and be a driving force over the next 15 years must it be adopt to the ever changing reality we live in. It's time for what I like to call Domain-Driven Design 4.0. The forces driving it are domain complexity and technology. More on that later.

Domain-Driven Design sprang out of Eric's experience developing business systems using object oriented languages during the late 1990ties. His experience was that developers and domain experts needed a common language to succeed, and that developers very often fell in love with the  technology, loosing out on the inherent complexity found in the domain at hand. The result was poor software quality, software that lacked the conceptual integrity required by a quality products.

Success was most often found in projects where the team had invested time digging into the domain and implemented the core domain concepts the products code base. The crux was to establish a common language that supported the communication between developers and domain experts. The developers stopped talking about database tables and rows and began talking about transfers of money, settlement of orders and cargo lifiting.

Another aspect was the architectural and technological landscape at the time. The PC had favoured a software architecture where a fat or rich clients accessed data stored in a relational database. Data gravity ensured that applications that started out small grew until the entropy got out of hand. It was always easier to add a new table than starting from scratch. Retrofitting old applications to work on the web using frameworks such as Enterprise Java din not help. In many ways they made things worse, moving focus away from the domain and to the technology.  

The programming styles emerging from the rich Windows clients propagated to the server side, following what Martin Fowler so brilliantly called the transactional script. These are GUI event handlers that tries to bring the effect of a mouse click to the database. To boost performance, critical business logic was moved from the client to the database using stored procedures maintaining the same programming style. I personally know systems where the database contain more than 1.5 million lines of PLSQL and have stored procedures more than 10.000 lines long.

Domain-Driven Design was born at a point in time where there was a strong belief in that object oriented programming thee mean to reduce complexity and boost developer productivity. The result we know, the ubiquitous language, context maps, core domain, supporting domain, entities, value objects, repositories, domain service, repository, factory, aggregates are all good helpers for those who was willing to invest in domain modelling and to bring the domain model into the code.

## Domain complexity
The British system thinker Derek Hitchins argue that complexity is perceived as a function of variety, connectedness and disorder. We perceive things as more complex if there is greater variety among components, more connections between components and the connections are tangled in stead of ordered.

Based on my experience as software architect and developer I will argue that we can argue that Hitchins wisdom materialises in what I will call structural and dynamic complexity. Structural domain complexity is the complexity we find in product structures suchas as an airplane, oil-rig, a retail assortment hierarchy or a project plan where we seek to find the critical path.

Dynamic domain complexity is s the result of dynamic intercourses between autonomous entities. This is the complexities we see in adversary games, on the battlefield, in human organisations and enterprise work patterns. Entities come and go, they might be lost to enemy action or connectivity loss.
the complexity we observe in adversary games, in warfare and enterprise work patterns. Here, objects collaborate, compete, form teams and even fight each other with effects that directly impacts their own and other objects possible courses of action.

The original DDD addresses structural domain complexity very well, but there is no directly expressed support for how to model dynamic domain behaviour. With IoT, AI and digitalisation and with the wish for DDD to be relevant in the future Domain-Driven design need to address both.

# Domain-Driven Design 4.0
Computing has experienced a profound change over the last 15 years, and there are at least three concerns that would benefit from being addressed in context of Domain-Driven Design.

Firstly, the cloud enables us to separate data from application, and to free us from the relational data model as the only storage model of business data. It's now possible to store data in fit for purpose data stores, it be graphs, key-value, relational or lake, and by doing so we are able to reduce the data gravity cost. This change will have a huge impact on how we address entities, value objects, repositories and aggregates. We can call this the data separation pattern or the master data repository.

Secondly, the real world consist of dynamic systems. Object oriented programming was created to  analysis of such systems. Business software developers has historically been spared from the challenges that comes from such systems. The closest they came was transaction processing. The Internet of Things changes this. Back-office processes must be able to respond to events at the edge, and they must be able to send new instructions to the edge process and devices. Architecturally this is solved using publish-subscribe and event processing.

Thirdly, new modern programming languages such as Swift unites object oriented programming and functional programming in ways that both supports and simplifies DDD. Remember, objects has state and functions are stateless. These properties become crucial when we are aiming at implementations of master data repository and concurrent asynchronous processes in a distributed environment. We need to implement rich domain models at both the edge and in the cloud.
 
With the scene set, let's roll.

## Masterdata, entities and repositories
Master data is defined as the business objects that contain the most valuable, agreed upon information that is shared across a business. Master data objects are the bearers of identity and lineage. In Domain-Driven Design Entities has this responsibility. Working with entities or master data objects implies working with who they are, not what they are and maintaining their identity and lineage across different bounded contexts.

The main difference between an entity and a master data object is that the scope of an entity is the local context, often defined by the boundary of an application. The scope of a master data object is enterprise wide and involves maintaining identity and lineage across multiple bounded contexts. The practical effect of this is that the footprint of the object is kept at a bare minimum. We could think of it as the super class every context specific instance inherits from. In many ways the top level generalisation.

In the upstream oil and gas "Well" is one of the core master data objects with a lifespan measured in decades. Well data is typically scattered over multiple data stores, each store using its own conventions, standards and encodings. This leads to a situation where identity and lineage is easily broken and keeping it intact become very expensive. 

Based on discussions with other oil companies we think the best way forward is to separate lifecycle management of master data objects from the applications using what we call a master data repository.

A master data repository provides a context independent home for the master data objects, maintaining its identity and lineage. In addition it will also hold meta data and reference data attributes, life-events and decisions. This move the management of identity and lineage out of the applications and to the repository, simplifying the concerns addressed by the  applications.

The master data repository API provide services for Ingestion, Search and Delivery. The internal representation of the repository matches best with a graph, where the objects life events are tracked and versioned accordingly with reference to where member data is stored. The master data repository ingestion and delivery service operates with aggregates. An aggregate understood as a clusters of entities and value objects with consistent boundaries that are managed as a whole.

On the client side, this makes a lot of things easier. The consuming contexts can focus on the processes, the workflows and the dynamic properties of the domain working with entities and value objects without being bothered with identity and lineage except as how these concerns materialises in the API. 
 
Processes, agents and dynamic domain modelling

Dynamic domain complexity can be seen as a collection of asynchronous, concurrent, competing and collaborating processes. 

Object oriented programming was created to study and analyse such processes in context of a system. A system being a part of the world that is regarded as a whole, with its interacting components.

For many reasons, it looks like the evolution of object oriented thinking stopped. The study of dynamic systems was left to the control theory community and artificial intelligence. The effect  was that the object world lost its connection with its origin.

In 1983 John Laired and Allen Newell created Soar, a cognitive agent architecture, and in 1991 Michael Bratman released his theory of human practical reasoning, also refers to as the BDI (Beliefs, Desires and Intentions) programming model for software agents.

In the simplest form: an agent have goals and execute plans to achieve those goals. Said in a simpler way, the agent execute actions as the response to external events. The hard part is the implementation of the agents reasoning leading to choosing the best possible action among many.

When late professor Kristen Nyggaard was teaching object oriented programming in his elder days, he used a restaurant as his example of a system and where he pointed out that processes has a set of basic qualities: Substance, state, transitions and structure. 

Using his own Cafe' Objecta as example, the substance is defined by guests, waiters, gatekeeper, cashier, bills, menus, food, tables and chairs. State refer to things like my table, my waiter, next in queue as well as a guests available funds, food names, queue lengths, expected waiting time and the actions performed by the objects to trigger and perform state changes. Transitions refers to things like seating, ordering, serving, eating and structure refers to the permanent properties of the process.

It can be argued that in any domain we find four types of objects, the object that does interesting things, the passive objects that provides basic services such as linked lists, queues and stacks. Then we have the objects that represents master data maintaining identity and lineage over time and lastly the objects that represents values and describe things ie. the value objects. The original book is weak when it comes to the objects that does interesting things, these are the objects that first and foremost represents processes, the objects that respond to events and performs actions or tasks.

Behaviour comes in four flavours. Firstly, we have simple behaviour represented by memoryless functions such as square root or an instruments measurement reading or sending an event. Secondly, we have state driven behaviours that most often are built on top of finite state machines. Thirdly, we have continuous behaviour found in digital filters, mathematical control systems, fuzzy logic and neural networks where the memory of historical events play a central role. Lastly, we have objects that have their own will, objects that controls their own thread of execution independent of the will of other objects. This group of objects are known as intelligent agents, they might represent roles and they might form organisational structures or teams that collaborate to achieve greater goals.

Architecturally behaviour could be modelled as a tasking model (Douglas) by asking the following questions. What are the work threads to be performed, what events triggers the work and what activities are performed as response to the triggers. What threads need to run concurrently and what type of race conditions and deadlocks might occur. The next step involves mapping tasks to objects. Doing that, we often end up with objects that have roles such as controllers, planners, observers or sensors. Two other concepts that might be helpful here is bounded contexts and micro-services as their unit of implementation.

It's beyond the scope of this essay to dig into the art of behavioural domain modelling beyond identifying its need and suggest some building blocks that might simplify the process as we move along.

Vernon in his Implementing Domain-Driven design supplements the toolkit with domain events, responsible for capturing something that happens in the domain. Calling a method on an aggregate root will of cause initiate a process inside the aggregate, a process that might propagate to other aggregates. This covers what we has identified as simple and state based behaviour.

In addition to the events we need the task model identifying the work items to be performed and we need to assign that work to objects responsible for making sure the work is performed. These objects comes in the flavour as controllers, planners, observers, sensors and even agents. The task model might also be a good start point for understanding what could be master data objects with identity and lineage. One way to approach that challenge is to adopt systems engineering (Hitchins) and the fact that there are always two systems in play: creating and created. We have the process of making a car and we have the car itself. Both might be master data objects that we want to track over time.

We need to make dynamic domain modelling a first class citizen of domain driven design and to do so we end up with five bearing concepts:

Agents as representatives of domain processes, controllers, observers, sensors and planners.
Events capturing the occurrences of something that happens in the domain (Vernon).
Tasks capturing the work to be performed by the process controller as response to a domain event.
Domain states capturing the state guiding the process representatives decision making.
Domain goals that defines domain process intended outcomes.
The internal substance and structure of objects that does interesting things can be complicated. Think of the domain model of an iPhone war game with its concurrency.

To support the design and implementations of these behavioural workhorses of your domain the GoF book provide several useful patterns such as: Chain of responsibility, Command, Observer and State. To study these patterns and others is highly recommended. For those who want to take it one step further "Doing hard time" (Douglas) is a good read.

Lastly, processes can be implemented in many ways. It can be the model in a iPhone application using grand dispatch, a Java Servlet, a Java thread, an Ada task or as a Unix cron job or whatever mechanism is provided by your platform of choice.

## Object-Functional languages
Functional programming goes back to lambda calculus, a formal system developed in the 1930ties to investigate computability, the Entscheidungsproblem, function definition, function application and recursion. Functional programming is declerative and have had its home ground in academia. Functional languages such as Haskell, F#, Clojure and Erlang have been used in industrial systems. JavaScript, one of the most used languages has the properties of a dynamically typed functional language in addition to the imperative and object oriented paradigme (Wikipedia).

Since 2003 several modern programming languages that supports both object oriented and functional programming has emerged and gained popularity. In addition to JavaScript we find Swift, Go and Scala to have mentioned some of them. I will use Swift as my foundation. 

In a functional language functions are first class citizens. Being a first class citizen enables the developers to use functions and methods like any other object or value. Functions can be passed as values, stored in properties and be returned as output from another functions. 

Swift make a clear distinction between reference types (class) and value types (enumerations, structs and tuples). Objects created as a reference type share a copy of the same instance.

class A { }

var a: A()

var b : A = a

Here both an and b refer to the same instance of A. The effect is that a change to variable a will impact variable b and vice versa.

Value types keeps a unique copy of its data.

struct B {}

var b: B()

var c : B = b

In this case variable c is made as a copy of b and they can be independently changed.

With functions as first class citizens they are just types and we can create structures where a function takes a function as input and returns a function as its output.

typealias Output = (Int) -> Int 

typealias Input = (Int, String, float) -> Bool

func doSomething(Input) -> (SomeType) { }

Another nice property that comes with functions is that they fit very well with multicore architectures, as we can execute them in their own threads in a safe way. Swift provides as an example a library called the Grand Dispatch that make concurrent programming using mulicore's a simpler feat than raw threads programming has proved to be.

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

Fowler, Patterns of Enterprise Applications.

Douglas, Doing hard time, Developing real-time systems with UML, Objects, Frameworks and Patterns.

Evans, Domain-Driven Design.

Vernon, Implementing Domain Drive Design.

Eidhof et al, Functional Swift.

Hitchins, Advanced systems, thinking, engieering and management.

Jarvis et al, Multiagent Systems and Applications: Volume 2: Development Using the GORITE BDI Framework.

Thanks to Alan Doniger, Shell for all interesting talks and discussions on data lifecycle management. The master data repository had not been possible without your contributions.


