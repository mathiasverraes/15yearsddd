# Distilling DDD into first principles

> “I don’t have talent, so I just get up earlier.” —Henry Rollins

If I could offer you one piece of advice (apart from always wear sunscreen), it would be to do your utmost to move beyond simply understanding your domain and get to a position where you are in sync with your business vision, goals, strategy and constraints. If you follow my advice then you should be in a position that not only gives you a deeper level of understanding for your domain enabling you to produce effective solutions, but will also allow you to proactively identify opportunities that offer true business value.

IT is now a crucial capability in any organisation. However most technical teams only seem to have a shallow understanding of the domain they work within and in my experience are more aligned to arbitrary requirements and new frameworks over the overall strategy and needs of a business. Advances in technology have afforded a huge amount of opportunity for business development and evolution however the majority of businesses are yet to catch up on these opportunities. This is not due to a lack of technical savviness from business colleagues but more from a lack of alignment from technical people, those that understand the art of the possible and the business needs, which prevents them seeing opportunities.

The line between the non technical and technical people within modern businesses is blurring. I am seeing more progressive companies that have blended roles where technical people have a seat at the table. They have a seat because they have earnt it and because they understand the art of the possible and how it will enable their company to beat the competition.

This essay is about my story and how DDD helped me learn more about solving problems and helping people to refocus efforts on how solutions are derived, how people  communicate and collaborate, how model-driven design is a collaborative process and how technical people can deliver solutions and identify opportunities that exceed expectations of business colleagues.

## Disclaimer

As this is all from my perspective it is heavily influenced by my own experience. I am not a consultant nor have I worked as a contractor so my experience is limited to the domains of e-commerce. However in my opinion these domains have been sufficiently complex and thus have benefited from applying the practices of Domain-Driven Design. 

I am not a jedi master in the art of Domain-Driven Design, I did not attend the Eric Evans finishing school (does that exist, if so please send me details) so I am unable to offer any words of wisdom less the ones that I have come to regard as lessons I have learnt. Over my career I have had the great fortune of working in a industry full of the most generous of people all over the world. The community of software is very good at offering opinions, advice and experience - all of which needs to be understood in the context that it is offered and of course moulded to the context that it will be applied in. A lot of what I have learnt and will write about is based on work by others, blog posts, peers, events - basically a great deal of what i know has been gained from standing on the shoulders of giants. I have made mistakes, many mistakes….an awfully large amount of mistakes. I have followed shiny new frameworks, jumped on the latest JavaScript framework bandwagon and jumped straight into an IDE before even finishing a conversation with a business counterpart. 

So while I can’t guarantee that my words of wisdom will fix all your problem I do hope you find something in the lessons that I have learned over the years that will act as a catalyst to helping you on your journey.


## The fundamental concepts of DDD

> Domain-driven design is both a way of thinking and a set of priorities, aimed at accelerating software projects that have to deal with complicated domains. Eric Evans, Domain-Driven Design (2003)

Before I talk about my takeaways from DDD and my view on the first principles I want to quickly recap on the fundamental concepts of Domain-Driven Design as it is often misunderstood when in my opinion it is deceptively simple. Of course the devil is in the detail.

DDD in a nutshell:

 * Distill a large problem domain into smaller subdomains. 
 * Identify the core sub domains. Those of greater value to focus effort and time
 * Collaborate with experts to build model that will provide solutions to solve problems or create opportunities in the core domain.
 * Split the model (if necessary) into smaller models where there is ambiguity in language, too large for a single team and enclose within a boundary to protect its context 
 * Implement the model in code using the same language as was used in the model. Use tactical patterns to separate technical code for domain code to prevent accidental complexity.

[show image of main points]


### Distill the Problem Domain to Reveal What Is Important

Development teams and domain experts use analysis patterns and knowledge crunching to distill large problem domains into more manageable subdomains. This distillation reveals the core sub domain—the reason the software is being written. The core domain is the driving force behind the product under development; it is the fundamental reason it is being built. DDD emphasizes the need to focus effort and talent on the core subdomain(s) as this is the area that holds the most value and is key to the success of the software.

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
 
To know where to focus effort you need to understand what makes the application worth designing in the first place. You need to understand the business strategy and why the existence of the software you are creating will enable it. It is worth asking why the custom software is being written rather than opting for a commercial off‐the‐shelf product. How will building an application make a difference to the business? How does it t within the strategy of the company? Why is it being built in‐house rather than being outsourced? Does part of the software give the business a competitive edge?

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


### Show passion for the problem domain

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

A software developer is primarily a problem solver who utilizes technology to implement a solution. Developers are fantastic at educating themselves on technology and project methodologies; however, decomposing a problem and being able to distill what is important from what is not will enable a good developer to become a great one. You should spend as much time in the problem space as you do in the solution space.

Just as a useful model is derived over a series of iterations, so too must a problem space be refined to reveal the true intent behind a stakeholder’s vision. Listening and drawing the why as well as the what and when from stakeholders is a skill that developers should practice just as they practice coding katas.
Code is a product of DDD, not the process; you can solve problems without having a technical solution.

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

All problems are not created equal; some are complex and are of little business value, so it makes no sense to waste effort in nding automated solutions for them. Complex edge cases do not always need automated solutions. Humans can manage by exception. If a problem is complex and forms an edge case, speak to your stakeholder and domain expert about the value of automating it. Your effort could be better served elsewhere, and a human might better handle this exception.

 * Avoid local optimisations at expense of improving the system
of 
 * Don’t solve all the problem
 * Will your output produce meaningful outcomes
 * Master the art of saying no. This will give you more time to focus on the strategic high value initiatives 
 * Curiosity and a genuine desire to learn about a problem space is vital to produce good solutions and meaningful software. In that you can produce elegant and beautiful software but if it provides no value or misses the point then it is utterly useless

### Reduce the cost of software 

 > “All good solutions have one thing in common: they are obvious but only in hindsight." Eli Goldratt

Teams that are aligned with the philosophy of DDD focus more on the bigger picture and understand where to put the most effort. They will not apply the same architecture to all parts of a solution, and they will not strive for perfection in areas of little value. They will trade isolated and working software for unnecessary elegance and gold plating.
Only the core domains need to be elegant due to complexity or importance. This is not to say that all other code should be poorly written, but it should be isolated, defined by a boundary, and expose behavior to support the core domain.

Applying techniques designed to manage complex problems to domains with little or no complexity will result in at best wasted effort and at worst needlessly complicated solutions that are difficult to maintain due to the multiple layers of abstractions. DDD is best used for strategically important applications; otherwise, the deep knowledge gained during DDD provides little value to the organization.
When creating a system, developers should strive for simplicity and clarity. Software that is full of abstractions achieves little more than satisfying developers’ egos and obscuring the reality of a simple codebase. Developers who aren’t engaged with delivering value and are instead only focused on technical endeavors will invent complexity because they’re bored by the business problem. This kind of software design can lead to frustration for teams in the future that need to maintain the mess of technical layers.

Don’t let design patterns and principles get in the way of getting things done and providing value to the business. Patterns and principles are guides for you to produce supple designs. Badges of honor will not be given out the more you use them in an application. DDD is about providing value, not producing elegant code.

Keep your model simple and focused, and strive for boring plain code. Often teams quickly fall into the trap of overcomplicating a problem. Keeping a solution simple does not mean opting for the quick and dirty; it’s about avoiding mess and unnecessary complexity. Use simplicity during code review or pair programming. Developers should challenge each other to ensure they are proving a simple solution and that the solution is explicitly focused only on the problem at hand, not just a general solution to a generalized problem.


* Simplify problems so that you can produce simpler solution models
* Don't gold plate software, good is often good enough - remember the goal.
* Nothing wrong with a hack if you excplicity understand the trade offs - story about EZY testing costs
* Software Is Just A Means To An End

### Explore alternative models

* Understand the Balance and Trade offs of alternative models - don't discount anything - outsource/data temps story
* Never say I know or stop at the first model

Only stop modelling when you have run out of ideas and not when you get the first good idea. Once you have a useful model start again. Challenge yourself to create a model in a different way, experiment with your thinking and design skills. Try to solve the problem with a completely different model. If you don’t get it right the rst time, refactor to a better solution. Constantly refactor to your understanding of the problem domain to produce a more express model. Models will change with more knowledge.

Remember a model is only useful for a moment in time; don’t get attached to elegant designs. Rip up parts of your model that are no longer useful, and be willing to change when new use cases and scenarios are thrown at your design.

Try to unlearn everything you gained for the first model and take a new direction. Explore and experiment to reveal insights and offer new solutions.
The result of tackling a problem from various angles is not the creation of a perfect model but instead the learning and discovery of concepts in the problem domain. This is far more valuable and leads to a team able to produce a useful model at each iteration.


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

Although having completely independent teams is a productivity win, it’s important to ensure that communication between teams still occurs for knowledge and skill‐sharing benets. Ultimately, bounded contexts combine at run time to carry out full use cases, so teams need a big‐picture understanding of how their bounded context(s) fit into the wider system. Established patterns for this problem involve having regular sessions in which teams share with other development teams what they are working on, how they have implemented it, or any technologies that have helped them achieve their goals. Another excellent pattern is cross‐team pair programming. This involves moving a developer
to a different team for a few days to learn about that part of the domain. You can spawn many novel approaches based on these two concepts of having group sessions and moving people around.


## Values

 > “Complaining does not work as a strategy. We all have finite time and energy. Any time we spend whining is unlikely to help us achieve our goals. And it won't make us happier.” ― Randy Pausch, The Last Lecture
 
 > "Complaining is not a strategy. You have to work with the world as you find it, not as you would have it be." —Jeff Bezos

* Have patience and humility
* respect others - people are good
* Avoid blaming

## To the next 15 years and the continued reinvention of DDD

* DDD is now an uncontrollable force. Even if you were to cut the head Evans, it would still continue to grow :)
* Future of DDD much more blending between developers and business people. Knowledgeable  IT people will turn into business decision makers
