# On objects, processes and data
#### From here to there and back again, Bilbo Baggins (Lord of the Rings)
## Foreword
With this essay I will try to be forward looking, while at the same time connect to the roots of object oriented programming and its true offspring domain driven design.

I will also like to thank Eric for his great contribution to software design and that he was able to articulate what object oriented programming was meant to be from its outset at University of Oslo back in the 1960ties.

Within the churning of change that surrounds us, also domain driven design itself need to be adapted to the new reality to stay relevant. 

I have pointed to three specific areas of concerns that I make domain driven design more important as we move forward into the unknown.

I will also like to thank Eric for all the great talks and discussions we had back in the days at then Statoil, now Equinor. We really plowed some new fields there. 

//Einar 

## Introduction
Fifteen years has passed since Eric Evans seminal book Domain Driven Design was published. Back then, there was no iPhone, no Facebook, no Netflix and Amazon had been profitable for two years. Windows 2000 was Microsofts flagship operating system, Sun Microsystems was a leading tech company, Java was 9 years old and the relational database ruled the enterprise data centers.

Developers could be found arguing over Java vs  C# and applications was still made in tools like Microsoft Access. Martin Fowlers Patterns of Enterprise Application Architecture was less than a year old and the GoF Design Patterns, Elements of reusable object-oriented software had just turned 9.

Since then, cloud computing, big-data, mobile-apps, internet of things, edge analytics, machine learning and artificial intelligence has become part of our professions vocabulary. New programming languages such as Swift, Scala and Go has entered the scene and old languages such as Python have resurrected to dominates data science. 

It is easy to argue that our profession is profoundly changed. Despite these changes, the principles and patterns of Domain Driven Design are still relevant and in many ways even more so as industry and society is digitalized and new business capabilities and models are built with software.

Technology has created new oportunities, oportunities that demands more from both developers and domain experts. There are more devices to program, multi-core processors in smart phones require skills in concurrent programming, the SQL database is replaced by a multitude of NOSQL storage oportunities. Open source software is used and found everywhere and the domain problems attacted with software are more suptle. 

For Domain-Driven Design to prosper and to be a driving force into the future must it be adapted to the changing reality of domain modelling. The time has come for what I like to call Domain-Driven Design 4.0. The forces driving this are found in increasing domain complexity in combination with evovling technology. More on that later. First a look at where we came from.

Domain-Driven Design sprang out of Eric's experience developing business systems using object oriented languages during the late 1990ties. His experience was that developers and domain experts needed a common language to succeed, and that developers very often fell in love with the  technology, loosing out on the inherent domain complexity. The result was poor software quality, software that lacked the conceptual integrity required by a quality product.

Success was most often found in projects where the team had invested in digging into the domain and implemented the core domain concepts in the products code base. The crux was to establish a common language that supported the communication between developers and domain experts. The developers stopped talking about database tables and rows and began talking about transfers of money, settlement of orders and cargo lifiting.

Another aspect was the architectural and technological landscape at the time. The PC had favoured a software architecture where a fat client accessed data stored in a relational database. Data gravity ensured that applications that started out small grew until the entropy got out of hand. It was always easier to add a new table than starting from scratch. Retrofitting old applications to work on the web did not help. In many ways they made things worse, moving focus away from the domain and to the technology and the complexities found in those frameworks.  

The programming styles from the rich Windows clients propagated to the server side, following what Martin Fowler so brilliantly called the transactional script. These are GUI event handlers that tries to bring the effect of a mouse click to the database. To boost performance, critical business logic was moved from the client to the database using stored procedures, while maintaining the same programming style. I personally seen stored database procedures more than 10.000 lines long.

Domain-Driven Design was born at a point in time where there was a strong belief in that object oriented programming was a silver bullet that would help reduce complexity and boost developer productivity. The result we know, the ubiquitous language, context maps, core domain, supporting domain, entities, value objects, repositories, domain service, repository, factory, aggregates are all good tools in the hands of those willing to invest in bringing the domain model into the code.

## Domain complexity
The British system thinker Derek Hitchins argue that complexity is a function of variety, connectedness and disorder. We perceive things as more complex if there is greater variety among components, more connections between components and the connections are tangled in stead of ordered. 

Having seen a multitude of domains over the years, I tend to think that domain complexity comes in two flavours; structural and dynamic, both deeply impacted by Hitchins thoughs on variety, connectedness and disorder. The big difference is where and how they materialises.  

Structural domain complexity is the complexity we find in product structures such as as an airplane, in a retail assortment hierarchy where we want to calculate margins, placements of items and item profitability, or in a project plan where we seek to find the critical path. The objects have high internal complexity in terms of complicated state models; sophisticated and changing business rules; involve deep data structures often produced by search; the need for lifecycle managment through versioning.

Dynamic domain complexity is the result of dynamic intercourses between autonomous entities. This is the complexities we see in adversary games, on the battlefield, in human organisations and enterprise work patterns. Objects come and go, they might be lost to enemy action or connectivity loss. They might collaborate, compete, form teams and the actions performed by one object have direct impact on other objects available options. The objects might have simple internal structures, but their interaction patterns are not.
 

# Domain-Driven Design 4.0
From the profound changes that have taken place since the book was written in 2003, there are three additional concerns that Domain-Driven Design need to address to stay relevant into the future. 

Firstly, the cloud enables us to separate data from application, and to free us from the relational data model as the only storage model of business data. It's now possible to store data in fit for purpose data stores, it be graphs, key-value, relational or lake. By doing so we are able to reduce the data gravity cost and it will impact on how we address entities, value objects, repositories and aggregates. We can call this the data separation pattern or the master data repository.

Secondly, the real world consist of dynamic systems. Object oriented programming was created to  analysis of such systems. Business software developers has historically been spared from the challenges that comes from such systems. The closest they came was transaction processing. The Internet of Things changes this. Back-office processes must be able to respond to events at the edge, and they must be able to send new instructions to the edge process and devices.

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
 
## Dynamic domain modelling
Dynamic domain complexity originates from asynchronous, concurrent, competing and collaborating processes that tries to get something done. Object oriented programming was created to study and analyse such processes in context of a system. A system being a part of the world that is regarded as a whole, with its interacting components.

Looking back, it looks like the development of object oriented thinking stopped. The object-oriented community was trapped in programming language features and object wiring techniques such as dependency inversion. The study of dynamic systems was left to the control theory and artificial intelligence communities. The effect was that the object world lost its connection with its origin. Very few think of software agents as objects on steroids. Objects are too bound to the "class" construct in your programming language of choice.

In 1983 John Laired and Allen Newell created Soar, a cognitive agent architecture and in 1991 Michael Bratman released his theory of human practical reasoning, known as the BDI (Beliefs, Desires and Intentions) programming model for software agents. Both BDI and Soar are domain models of how the human brain reasons and transfer perception into action.

Intelligent agents is the cornerstone of artificial intelligence that comes in many flavours, spanning from Bots to space crafts. An intelligent software agent is a program that solves problems, a program that perform work. Agents can act in roles and it can collaborate and interact with other agents including humans. Agents are objects that control their own execution thread, they are active, they observe their environment and pursues intents. They can be reactive and proactive, they can learn and they can make plans.

The code sniplet below illustrate how tightly relatated agents and objects are.   

	public class Agent implements Runnable {
	    
	    public void run() {
		while true {
	   	  // Percept environment
	   	  // Choose and perform action
		  // Update state
		}
	    }
	}

The hard part is the implementation of the agents reasoning method or agent function (Russel&Norvig) that maps a given perception with the best possible action. Multi-agent frameworks such as JACK, BDI4Jade and Gorite simplifies that part of the job as they implement the domain language of their respective cognitive architectures.

When late professor Kristen Nyggaard was teaching object oriented programming he used Cafe' Objectas as an example of a system that contained processes defined by a set of basic qualities: Substance, state, transitions and structure.
- Substance was defined by Guests, Waiters, Gatekeeper, Cashier, bills, menus, food, .. 
- State refer to things like my table, my waiter, next in queue and available funds. 
- Transitions refers to things like seating, ordering, serving, eating. 
- Structure refers to the permanent properties of the process.
I included this to show that behaviour modelling was at the core of object oriented programming.

When observing Cafe' Objecta as a dynamic system we easilly see the objects involved in doing interesting things such as Waiter, Guest, Gatekeeper and Cashier and the objects that describe and define things such as Menus, Food, Bills and Tables.

Objects whos primary role is to do things are best understood as intelligent agents. To classify an agents cognitive and behavioral capability as implemented by the agent function can be done using a stack model:

- Reasoning based behaviour implemented using cognitive architectures such as BDI and Soar.
- Continous behaviour found in digital filters, mathematical control systems, fuzzy ogic and neural networks, behaviour where the memory of historical events play a central role in the agents decision making process.
- State driven behaviour, typically built from finite state machines (value objects).
- Simple behaviour represented by memoryless functions such as calculating the square root or reading a measurement.

Behavioral modelling starts with the tasking and event model: What are the tasks to be performed? What event triggers the need for a certain task? What is the intended outcome from a task? What messages are sent and who are the recievers? Who performs the task? What events are created by executing tasks?

When developing a tasking and event model there is two vital factors to consider: firstly, what tasks will be performed concurrently and will they compete for the same resource? If yes, than we are heading toward race conditions and possible deadlocks in the realm of concurrent programming. Secondly, if there are tasks with time budgets i.e. tasks must be completed within given time windows we are in the realm of real-time systems. 

To sum up. Dynamic domain modelling must become a first class citizen of domain-driven design, and to support that new citizen we need four new concepts that become part of the Domain-Driven Design toolbox:

- Tasks defines the work to be performed by the agents.
- Agents characterizes the objects whos primary task is to perform tasks.
- Agent function defining the agents mapping of perceptions to tasks.
- Events capturing the triggers for a task to be performed

For those who want to take it one step further Douglas, Russel & Norvig and Jarvis et al are good reads.

## Object-Functional languages
Functional programming goes back to lambda calculus, a formal system developed in the 1930ties to investigate computability, the Entscheidungsproblem, function definition, function application and recursion. Functional programming is declerative and have had its home ground in academia. Functional languages such as Haskell, F#, Clojure and Erlang have thoug been used in industrial systems. JavaScript, one of the most used languages has the properties of a dynamically typed functional language in addition to its imperative and object oriented paradigme (Wikipedia).

Since 2003 several modern programming languages that supports both object oriented and functional programming has emerged and gained popularity. In addition to JavaScript we find Swift, Go and Scala to have mentioned some of them. I will use Swift to illustrate the possibilities.

In a functional language functions are first class citizens. Being a first class citizen enables the developers to use functions and methods like any other object or value. Functions can be passed as values, stored in properties and be returned as output from another functions. 

Swift make a clear distinction between reference types (class) and value types (enumerations, structs and tuples). Objects created as a reference type share a copy of the same instance.

	class A { }
	var a: A()
	var b : A = a

Both an and b refer to the same instance of A. The effect is that a change to variable a will impact variable b and vice versa. In program stuctures of some size this easily become a problem. One way to deal with that problem is to make the class immutable by decklaring members as constants in stead of as variables.

Swift provdes three value types, struct, enumeration and tuples that keeps a unique copy of its data. In context of domain driven design this is an enrichment of the ubiqitous language. We are given a richer toolbox as illustrated by the code below where we build a domain model of a door in a house using the different language constructs.

	enum DoorState {
	   case open
	   case closed
	}
	
	struct Door {
    	    let state : State
	    init() {
	    	state = State.closed
	    }
	    init(_ state: State) {
	     	self.state = state
	    }
	    
    	    func open() -> Door {
        	return Door.init(State.open)
	    }
    
	    func close() -> Door {
        	return Door.init(State.closed)
    	    }
	}

	class House {
	   var frontDoor = Door()
	   func openFrontDoor() {
	        frontDoor = frontDoor.open()
	   }
	   
	   func closeFrontDoor() {
	   	frontDoor = frontDoor.close()
	   }   
	}
	
	// Using the house class
	var myHouse = House()
	myhouse.openFrontDoor()

The house maintains its own state. The state can be changed by invoking methods on the house object. This illustrates how the static domain complexity materialises. We add more doors, windows and a heating system and rules we see how the structural complexity grows.

In Swift functions are first class citizens. They are types which means that functions can be passed around in the ways as classes and structs. Functions can take functions as input paratmeters as well as output and they can be stored in variables and constants. This is illustrated in the code below. 


	typealias MathFunc = (Int, Int) -> Int

	func multiplyTwoInt(_ a: Int, _ b: Int) -> Int {
    	   return a*b
	}

	func addTwoInts(_ a: Int, _ b: Int) -> Int {
    	  return a + b
	}

	enum MathOps {
    	   case add
    	   case multiply
	}

	func mathFuncFactory(_ ops: MathOps) -> MathFunc {
    	   switch ops {
    	      case .add:
        	return addTwoInts(_:_:)
    	      case .multiply:
        	return multiplyTwoInt(_:_:)
   	    }
	}

	var adder = mathFuncFactory(MathOps.add)
	var multiplier = mathFuncFactory( MathOps.multiply)
	var mathFunction:  MathFunc = addTwoInts

	func printResult(f: MathFunc, _ a: Int, _ b: Int) {
    	    print("Result: \(f(a,b))")
	}

	printResult(f: addTwoInts, 3,5)
	printResult(f: multiplier, 5,5)
	printResult(f:mathFuncFactory(MathOps.add),3,10)

Another nice property that comes with functions is that they fit very well with multicore architectures, as they can be executed in their own concurrent thread. Swift provides a library called the Grand Dispatch that simplify concurrent programming using mulicore's compared with raw threads programming.

Entities are defined as objects known defined by their identity and their lineage. They are most often best implemented as a reference type (class). Their identity should come from their standing in the business, and they should just conform to a protocol as illustrated below.

	protocol Entity {
	    var identity : Int { get } 
	    func equals(Entity) -> Bool
	}

	class Well: Identity {
	   internal var identity = 1000 
	   func equals(_ entity: Entity) -> Bool { 
	      	return self.identity == entity.identity
	   }
	   
	   // Useful code here
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

Russel, Norvig, Artifical intelligence, A modern approach, third edition

Thanks to Alan Doniger, Shell for all interesting talks and discussions on data lifecycle management. The master data repository had not been possible without your contributions.


