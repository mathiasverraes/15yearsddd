# Distilling DDD into first principles

* My personal context, my journey, introduction and experience of DDD
* Why I am not a jedi master - I only know the domains I know
* First principle - DDD - Drive all design decisions based on the rule “will this help achieve the goal?”

## The fundamental concepts of DDD

> Domain-driven design is both a way of thinking and a set of priorities, aimed at accelerating software projects that have to deal with complicated domains. Eric Evans, Domain-Driven Design (2003)

Before I talk about my takeaways from DDD over the past 13 years I want to quickly recap on the fundamental concepts of Domain-Driven Design as it is often misunderstood when in my opinion it is deceptively simple.

### Distill the Problem Domain to Reveal What Is Important

 * Core domain and sub domains

### Create models to solve problems

 * Model-driven design

### Apply Bounded Contexts to Isolate Models from Ambiguity and Corruption

 * Bounded contexts 

### Understanding the Relationships between Contexts

 * Contexts Map
 * Tech relationships
 * People relationships

### Employ tactical patterns to separate technical complexity from domain logic complexity in the code model

 * Code patterns

## So what? I already knew this stuff

As you will have noticed the majority of effort when applying the practices of Domain-Driven Design lie outside of the technical realm. Before one can code a solution one must truly understand the problem. These non technical aspects are what I refer to as the first principles of Domain-Driven Design. Many people’s first introduction with Domain-Driven Design is an exposure to the tactical design patterns as well as techniques such as event sourcing and CQRS. However it is the deep understanding of the problem space and the relentless focus on the core domain that allow effective and collaborative model-driven design to lead to a viable solution. Only then do we need to leverage tactical patterns to organise code in such a manner as to reduce accidental complexity.

### Striving for Tactical Pattern Perfection
Teams concerned only with writing code focus on the tactical patterns of DDD. They treat the building block patterns as a bible rather than a guide, with no understanding of when it’s okay to break the rules. They spend wasted effort adhering to the rules of the patterns. This energy is better spent on understanding why it needs to be written in the rst place. DDD is about discovering what you need to write, why you need to write it, and how much effort you should use. As mentioned before, the tactical patterns of DDD are the elements that have evolved the most since Eric’s book was written, with the strategic side of DDD remaining faithful to Eric Evan’s original text. How development teams create domain models is not nearly as important as understanding what models to write in the rst place and how to develop them in a bounded context. Understanding the what and the why of problem solving is a more important process than how you are going to implement it in code.

### Why sample applications don’t tell the full story
One of the most often-asked questions on software development forums is this: Can I see a sample application? There are probably many good solutions that show the result of a product developed under a DDD process, but much of the benet of DDD is not revealed when you only examine the code artifact. DDD is performed on whiteboards, over coffee, and in the corridors with business experts; it manifests itself when a handful of small refactorings suddenly reveal a hidden domain concept that provides the key to deeper insight. A sample application does not reveal the many conversations and collaborations between domain experts and the development team.

The code artifact is the product of months and months of hard work, but it only represents the last iteration. The code itself would have been through a number of guises before it reached what it resembles today. Over time, the code will continue to evolve to support the changing business requirements; a model that is useful today may look vastly different to the model used in future iterations of the product.

If you were to view a solution that had been built following a DDD approach hoping to emulate the philosophy, a lot of the principles and practices would not be experienced, and too much emphasis would be placed on the building blocks of the code. Indeed, if you were not familiar with the domain, you would not find the underlying domain model very expressive.
DDD does prescribe a set of design best practices, patterns, and building blocks that are often mistakenly thought to be core to applying DDD to a product. Instead, think of these design artifacts
as merely a means to an end used to represent the conceptual model. The heart of DDD lies deep in the collaboration between the development team and domain experts to produce a useful model.

### Don't miss the real vale of DDD
A team focusing too much on the tactical patterns is missing the point of DDD. The true value of DDD lies in the creation of a shared language, specific to a context that enables developers and domain experts to collaborate on solutions effectively. Code is a by-product of this collaboration. The removal of ambiguity in conversations and effortless communication is the goal. These foundations must be in place before any coding takes place to give teams the best chance of solving problems. When development does start to focus on language, context and collaboration enable code to be well organized and bound to the mental models of the business.
Problems are solved not only in code but through collaboration, communication, and exploration with domain experts. Developers should not be judged on how quickly they can churn out code; they must be judged on how they solve problems.

### Going Back to First Principles
The remainder of this essay focuses on distilling the non technical aspects DDD down into first principles that I have learned to focus on over my time working in software development. 

[Show mind map/image of techniques available to do the fundamentals.]

I would hasten to add that however well you manage the non technical side you it goes without saying you need to have a proficient technical ability. However I have often witness that a good understanding of the goal of the core domain and the problem space itself enable a simpler solution to be found that requires a simpler technical implementation. Again as I mentioned at the start of this essay, I can only write from my perspective and from the experience of the domains that I have worked within. Remember its all about context, and this is mine.


## Gain agreement on the problem

 > “If you do not deal directly with the core problem, don’t expect significant improvement.” —Eli Goldratt

 * Understand the business big picture (problems, constraints, opportunities)
 * Distil large problem into sub domains
 * Core domain, the goal, or impediment is revealed to give focus and alignment
 * Look for interesting problems - sometimes we don't know the exact details of the problem or how to solve it. We must work with non technical people to look for opportunity. 
 * For example - problem is we are 10% down on budget. Explore how to solve.

 
 ### Applying the Theory of Constraints to reveal impediments to business value throughput

 * Shift focus from local optimisations to increasing the flow of the system
 * For example 2nd class shipping postage may save money but is uncompetitive and will lose sales and hit revenue line.
 * Remove impediments to producing business value

### Be clear on how you deliver business value

 * Value solutions over software. It’s not about being a code monkey it’s about getting results
 * Being clear on what business value is helps to identify if a problem is worth solving or is valuable
 * Look for the money / how does it shift the KPI
 * People don't want to buy a quarter-inch drill, they want a quarter-inch hole - nobody cares how well crafted your code is unless is makes money
 * Look for the money / how does it shift the KPI / where is the bottleneck to business throughput
 * Delivering Business Outcomes over code output / Value solutions over software
 * IT more than ever is at heart of business success. IT people that understand this transforms businesses. Seat at the table
 * IT has a greater amount of power and influence than before. New business models can be developed through leveraging technology. Teams should act like commercially and be business (domain) focused.
 * Avoid software being what developers understand from the business - developers ARE the business.
 * Your job is to Remove blockers from business value throughput

## Collaborate on the direction for a solution

 * Collaborate on the direction for a solution with decision makers and experts, people that are passionate about the problem space
 * Model-Driven Design
 * Collaboration is key. Don’t sit and wait for requirements - offer solutions. Don’t leave it to others. If you know the goal and know the business and can do IT you can offer solutions rather than waiting to be asked.
 * What is the definition of an Analyst programmer? An analyst is an individual who performs analysis of a topic
 * Offer opportunities / art of the possible before you are asked - be proactive
 * Have lots of ideas / models
 * Data entry example. Don’t assume anything - don’t think oh it doesn’t use code!


### Show a professional passion for the problem domain

 * Don’t stop asking questions!
 * You cannot begin to be useful to solve a problem or look for opportunity if you don't really understand the domain you are working in to a sufficiently deep level
 * Have passion for the problem space - this will make it easier to find solutions and more importantly opportunities
 * Focused  (Dan North) Deliberate Discovery at the constraint/bottleneck
 * You are a professional. You are paid well. You have a responsibility to understand the domain you are in.
 * You don’t need to show empathy, you need to enable your business! You need to show solidarity to help your business
 * Be proactive, be curious
 * Don’t accept mediocrity in business process
 * Programming is understanding and translating into a software specific language. The software proves our understanding.

### Collaborate on viable solutions rather than looking for requirements 

 * Requirements assume someone has all the answers - this is a massive fallacy. Not about getting requirement. Remove problems with business counterparts or show art of the possible, look for opportunities.
 * Be accountable, don't be lazy - Don’t delegate solution design to the business. It’s not someone else’s problem, it’s yours.
 * IT is the business
 * Domain experts are not system experts. Learn and discover with them. IT + Domain experts + decision makers = solutions
 * If you not making a difference then what are you doing
 * Be empowered
 * Domain experts are not system experts. Learn and discover with them
 * IT + Domain experts + decision makers = solutions
 * Don’t settle for meetings without meaning and that won’t progress your understanding. Get decisions made.
 * I have often found it the case that domain experts don’t know how current system. They are domain experts, experts in there fields, but not business process engineers, not systems experts 

### Learn to Facilitate Problem exploration

 > “Engagement is more important than precision.” Alberto Brandolini on Event Storming

 * Visualise and reveal with Process mapping or event storming big picture
 * Requires decision makers and domain experts. Help good decisions get made.
 * You don't need to be smartest, need to enable

## Gain agreement that the solution solves the core problem

 > “Technology can bring benefits if, and only if, it diminishes a limitation.” —Eli Goldratt


### The Jurassic Park Principle

 > "Your scientists were so preoccupied with whether or not they could that they didn't stop to think if they should.” Dr. Ian Malcom, Jurrasic Park

 * Avoid local optimisations at expense of improving the system
of 
 * Don’t solve all the problem
 * Will your output produce meaningful outcomes
 * Master the art of saying no. This will give you more time to focus on the strategic high value initiatives 
 * Curiosity and a genuine desire to learn about a problem space is vital to produce good solutions and meaningful software. In that you can produce elegant and beautiful software but if it provides no value or misses the point then it is utterly useless

### Reduce the cost of software 

 > “All good solutions have one thing in common: they are obvious but only in hindsight." Eli Goldratt

* Simplify problems so that you can produce simpler solution models
* Don't gold plate software, good is often good enough - remember the goal.
* Nothing wrong with a hack if you excplicity understand the trade offs - story about EZY testing costs
* Software Is Just A Means To An End

### Explore alternative models

* Understand the Balance and Trade offs of alternative models - don't discount anything - outsource/data temps story
* Never say I know or stop at the first model

## Optimize for the Overall System 

 > “A company could put a top man at every position and be swallowed by a competitor with people only half as good, but who are working together.” W. Edwards Deming

 * Not the Individual Components
 * Understand how you fit into to the system

### Manage the solution team organisational design for autonomy 

  * Product Teams
  * Capability Teams
  * Ownership and accountability
  * Loosely coupled but highliy cohesive -  understanding of the business capabilities
  * Align with business process ownership
  
### Identify constraints in delivering the solution 

* Constraints outside  IT, vendors and business colleagues
* Obsess over dependencies
* simplify relationships. 

### Collaborate to solve the big picture

* Always keep a eye on the goal/bottleneck
* Context Maps important but also use process maps to understand system flow
* Ensure all teams are aligned by understanding the goal,  collaborate together on a solution and understand how they fit into the bigger picture 

## Values

 > “Complaining does not work as a strategy. We all have finite time and energy. Any time we spend whining is unlikely to help us achieve our goals. And it won't make us happier.” ― Randy Pausch, The Last Lecture
 
 > "Complaining is not a strategy. You have to work with the world as you find it, not as you would have it be." —Jeff Bezos

* Have patience and humility
* respect others - people are good
* Avoid blaming

## To the next 15 years and the continued reinvention of DDD

* DDD is now an uncontrollable force. Even if you were to cut the head Evans, it would still continue to grow :)
* Future of DDD much more blending between developers and business people. Knowledgeable  IT people will turn into business decision makers
