# Agents, Domain objects on steroid
#### From here to there and back again, Bilbo Baggins (Lord of the Rings)
## Introduction
This essay explains dynamic domain modelling and argue why we need to make it a first class citizen of Domain-Driven design.

Before that, I will  like to thank Eric for his seminal contribution to the software community. I will also like to thank him for all the great discussions we had back in the days when we were battling Equinor's (the Statoil) oil trading portfolio.

Fifteen years has passed since the book was published. Back then, there was no iPhone, no Facebook, no Netflix and Amazon had been profitable for two years. Windows 2000 was Microsofts flagship operating system, Sun Microsystems was a leading tech company, Java was 9 years old and the relational database ruled the enterprise data centres.

Since then, cloud computing, big-data, mobile-apps, internet of things, edge computing, machine learning and artificial intelligence has become part of our professions vocabulary. New programming languages such as Swift, Scala and Go has entered the scene and old languages such as Python have resurrected and dominates data science.

It is easy to argue that our profession experience profound changes, changes that I think make Domain-Driven design even more important, changes that also require Domain-Driven design itself to change, adopting itself to the needs of a software defined world.

## Domain complexity
The British system thinker Derek Hitchins argue that complexity is a function of variety, connectedness and disorder. We perceive things as more complex if there is greater variety among components, more connections between components and the connections are tangled instead of ordered. 

Combining his thoughts with my own experience, I think domain complexity falls into one of two buckets; its structural or dynamic.

Structural domain complexity is what we find in nested structures such as as an airplane, a retail assortment hierarchy or in a project plan. The objects involved become complicated due to their internal state models, their rules and the depth of their connectedness. 

Dynamic domain complexity comes from the intercourses between autonomous components or objects. This is the complexities we find in dynamic systems. The complexity is not found on the objects inside, but in their ever changing interactions and arbitrary connectedness.

Objects come and go, they might be lost to enemy action or communication loss. They might collaborate, compete, form teams and actions taken by one object have direct impact on other objects available options. 

Domain-Driven design addresses structural complexity. Entities, value objects, aggregates, repositories and services are structural building blocks that helps us to create order, reduce connectedness easing the management of variability. 

Dynamic complexity is not addressed at all. Vernon introduces domain events in his book. That is a good start but the challenge is deeper than events and the benefits bigger.

## Agents
The real world consist of dynamic systems. Dynamic domain complexity originates from asynchronous, concurrent, competing and collaborating processes.

Object oriented programming was created to study and analyse processes in context of a system through simulation, directly supported by the Simula 67 language. The object oriented software community lost its interest in dynamic systems as it turned itself to programming languages. The study of dynamic systems was left for the control theory (cybernetics) and artificial intelligence (AI) communities. 

It's worth mentioning that control theory and AI are siblings, both conceived at workshops in the late 1940ties. The differencing factor was that control theorists lent themselves to calculus and matrix algebra and the problems suited for that approach i.e. systems described by fixed set of continuous variables. The AI group did not accept that limitations and chose the tools of logical interference and computation, allowing them to consider problems such as language, vision and planning.

In the AI community the ideas of rational actions led to rational agents (agere Latin for to do) aka intelligent agents i.e. computer programs that does work. Of cause, all programs does work, but agents are expected to do more: operate autonomously, persist over time, adapt, change and create and pursue goals. A rational agent is an agent that acts to achieve the best possible outcome (Russel & Norvig).

An intelligent agent is a program that solves problems by observing an environment and execute actions toward that environment. Agents can act in roles, collaborate and interact with other agents including humans. 

Software wise are intelligent agents objects that control their own execution thread, they are active, and they do interesting things. The problem though, very few see agents as domain objects on steroids. How easy it is to create a software agent is illustrated in the Java code below.   

	public class MyAgent implements Runnable {
	    
	    public void run() {
		while true {
		   // Percept environment
		   // Select and execute action
		   // Update internal state
		}
	    }
	}

Intelligent agents is the cornerstone of artificial intelligence. They come in many flavours, spanning from Bots to space crafts and they are the key to autonomous systems.

The hard part is the implementation of the agents reasoning method or agent function (Russel & Norvig), mapping a given perception or goal with the best possible action. Agent functions can be very simple or very sophisticated and they can be sorted into a capability stack:

- Reasoning based behaviour implemented using cognitive architectures such as BDI and Soar.
- Continuous behaviour found in digital filters, mathematical control systems, fuzzy logic and neural networks, behaviour where the memory of historical events play a central role in the agents decision making process.
- State driven behaviour, typically built from finite state machines (value objects).
- Simple behaviour is represented by memoryless functions such as calculating the square root or reading a measurement.

The most sophisticated agent functions implies use of cognitive architectures such as Soar and BDI. Soar was created in 1983 by John Laired and Allen Newell and is now maintained by Laird's research group at University of Michigan. BDI or more precisely Beliefs-Desires-Intentions was created in 1991 by Michael Bratman in his theory of human practical reasoning.  

Soar and BDI are domain models of how the human brain reasons and transfer perception into action. Both architectures are supported by open-source and commercial implementations such as JACK, BDI4Jade, Gorite and SOAR. 

## Dynamic domain modelling
Late professor Kristen Nygaard used Cafe' Objecta as his system metaphor when teaching object oriented programming. When observing Cafe' Objecta we find objects who does interesting things such as Waiter, Guest, Gatekeeper and Cashier and objects that define and describe things such as Menus, Food, Bills and Tables. 

Behavioural modelling is about the objects that does interesting thing and it begins with the development of the tasking and event model (Douglas): What are the tasks to be performed? What event triggers the need for a certain task? What is the intended outcome from a task? What messages are sent and who are the receivers? Who performs the task? What events are created by executing tasks?

When developing a tasking and event model there is two vital factors to consider: firstly, what tasks will be performed concurrently and will they compete for the same resource? If yes, then we are heading toward race conditions and possible deadlocks and we need concurrent programming skills. Secondly, if there are tasks with time budgets i.e. tasks must be completed within given time frames we need real-time system skills.

To support the modelling of dynamic systems we need to add four concepts to our Domain-Driven Design toolbox:

- Tasks, the work to be performed by the agents.
- Agents, the objects who's primary task is to perform tasks 
- Agent function, how the agent maps it's perceptions to tasks.
- Events, the things happens that triggers the need for a task to be performed.

By making these four first class citizens of Domain-Driven design we are well off.

Some might ask, what differs an agent from a micro-service? My answer is granularity. Agents are objects, they are in the end defined by the class constructor in the language of choice.

For those who want to take it one step further Douglas, Russel & Norvig and Jarvis et al are all good reads. Hitchins for the special interested. An I expect that all of you have read Eric or Vernon's books.


## Reflections
If your domain problem is best solved using a cognitive architecture, the advice is to look for an established framework. No reason to build this yourself.

Why now? 
- The Internet of Things and the move toward the software defined world changes the rules for business software. Back-office processes must be able to respond to events at the edge, and they must be able to send new instructions to the edge process and devices in real time. 
- Automation of work begins with capturing the tasks.
 
I hope you now understand agents as first class citizens of many domains, and that they are domain objects on steroids.

## References
- Douglas, Doing hard time, Developing real-time systems with UML, Objects, Frameworks and Patterns.
- Evans, Domain-Driven Design, Tackling the complexity at the heart of software.
- Hitchins, Advanced systems, thinking, engineering and management.
- Jarvis et al, Multiagent Systems and Applications: Volume 2: Development Using the GORITE BDI Framework.
- Russel, Norvig, Artificial intelligence, A modern approach, third edition.
- Vernon, Implementing Domain Drive Design.

