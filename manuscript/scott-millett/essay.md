# Distilling DDD Into First Principles — Scott Millett

*Parts of this essay first appeared in the book Patterns, Principles, and Practices of Domain-Driven Design (Wrox 2015) by Scott Millett and Nick Tune.*

If I could offer you one piece of advice (apart from always wear sunscreen), it would be to do your utmost to move beyond simply understanding your domain and get to a position where you are in sync with your business vision, goals, strategy and constraints. You should share the same worries as your business counterparts: are we going to hit budget? how do we successfully launch our proposition in a new territory? how do we remove the bottleneck in fulfillment? If you are able to move to a more fundamental level of understanding for your business then you should be in a position that not only gives you a deeper level of understanding for your domain, enabling you to produce effective solutions, but will also allow you to proactively identify product opportunities that offer true business value.

It should come as no surprise to you that software is eating the world and that IT is now a crucial capability in any organisation. However most technical teams only seem to have a shallow understanding of the domain they work within and in my experience are more focused on tech for tech’s sake over the overall strategy and needs of a business. Advances in technology have afforded a huge amount of opportunity for business development and evolution, however the majority of businesses are yet to catch up on these opportunities. This is not due to a lack of technical savviness from business colleagues but more from a lack of alignment from technical people, those that understand the art of the possible, which prevents them from seeing opportunities.  

The line between the non-technical and technical people within modern businesses is blurring. I am seeing more progressive companies that have blended roles where technical people have a seat at the table. They have a seat because they have earnt it through leveraging the art of the possible, technical opportunities, to remove a constraint on the production of business value. They are aligned to the real needs of the business and they have the autonomy to deliver solutions to meet those needs.

This essay is about my story and how DDD helped me learn more about solving problems and helping people to refocus efforts on how solutions are derived, how people  communicate and collaborate, and how technical people can deliver solutions and identify opportunities that exceed expectations of business colleagues. 

![Be the art of the possible](images/scott-millett/artofthepossible.png)

## Disclaimer

> “I don’t have talent, so I just get up earlier.” —Henry Rollins

This essay is all from my perspective and therefore it is heavily influenced by my own experience. I am not a consultant nor have I worked as a contractor so my experience is limited to the domains of e-commerce in one flavour or another. However in my opinion these domains have been sufficiently complex and thus have benefited from applying the practices of Domain-Driven Design. I am not a jedi master in the art of Domain-Driven Design, I did not attend the Eric Evans finishing school (does that exist? If so please send me details) so I am unable to offer any words of wisdom less the ones that I have come to regard as lessons I have learnt. 

Over my career I have had the great fortune of working in a industry full of the most generous of people from all over the world. The community of software is very good at offering opinions, advice and experience - all of which needs to be understood in the context that it is offered and of course moulded to the context that it will be applied in. 

So while I can’t guarantee that my words of wisdom will fix all your problems (or any), I do hope you find something in the lessons that I have learnt over the years that perhaps can act as a catalyst to helping you on your DDD journey. However do remember, its all about context, and this is mine.

## The Fundamental Concepts Of DDD

> Domain-driven design is both a way of thinking and a set of priorities, aimed at accelerating software projects that have to deal with complicated domains. Eric Evans, Domain-Driven Design (2003)

Before I talk about my takeaways from DDD and my view on the first principles I want to quickly recap on the fundamental concepts of Domain-Driven Design as it is often misunderstood when in my opinion it is deceptively simple. Of course the devil is in the detail. 

DDD in a nutshell:

 * Distill a large problem domain into smaller sub domains.
 * Identify the core sub domains to reveal what is Important. The core domains are those of greater value to the business which require more focus, effort and time.
 * Collaborate with experts to discover an analysis model that will provide solutions to solve problems or reveal opportunities particularly in the core domain.
 * Use the same ubiquitous language to bind the analysis model to the code model. Use tactical patterns to separate technical code from domain code to prevent accidental complexity.
 * Split the model (if necessary) into smaller models where there is ambiguity in language or the model is too large for a single team. Enclose the model within a boundary to protect the models integrity. When working with multiple models it's  important that they are understood in context.
 * Keep a context map to understand the relationships, social and technical, of all models in play.


![Overview of Domain-Driven Design](images/scott-millett/01_DDD_Overview.png)


### Distill The Problem Domain To Reveal What Is Important

Development teams and domain experts use analysis patterns and knowledge crunching to distill large problem domains into more manageable sub domains. This distillation reveals the core sub domain(s)—the reason the software is being written. The core domain is the driving force behind the product under development. For example in a airline pricing system the algorithm could be the key to the software being successful or not. The system would of course need identity and access control management but this would only be to support the core domain. In a different domain, say government documentation control the security and access may be the core domain and management of content only supporting. The point is that DDD emphasizes the need to focus effort and talent on the core sub domain(s) as this is the area that holds the most value and is key to the success of the software.

### Create Models To Solve Problems

With an understanding of where to focus effort, the technical team along with domain experts can begin to derive a solution represented as an analysis model. This is typically done in a collaborative manner occuring around whiteboards, working through concrete scenarios with business experts and generally brainstorming together. This process is the catalyst to conversation, deep insight, and a shared understanding of the domain for all participants. It is the quest to discover and agree on a shared understanding of the problem domain to produce a model, using a shared, ubiquitous Language,  that can fulfill business use cases, remove constraints or open up opportunities. 

When a useful analysis model is discovered a code model can follow. I hasten to add that this process is not as linear as I am explaining here and often a code model is used during model exploration to prototype ideas in code to understand feasibility. The code model is to bound to the code analysis model via the use of a shared, or as DDD refers to it a Ubiquitous Language. The Ubiquitous Language ensures that both models stay in sync and are useful during evolution. Insights gained in either model are shared and knowledge is increased, leading to better problem solving and clearer communication between the business and development team.

Tactical patterns are used to keep the code model supple and to isolate domain from infrastructure code thus avoiding the accidental complexity of merging technical and business concerns. 

### Split Large Models To Prevent Ambiguity And Corruption

Large models can be split into smaller models and defined within separate bounded contexts to reduce complexity where ambiguity in terminology exists or where multiple teams need to work in parallel. The bounded context defines the applicability of the model and ensures that its integrity is retained. The bounded contexts form a protective boundary around models that helps to prevent software from evolving into a big ball of mud. Context boundaries aren’t limited to just language or team set up. They can be influenced by ambiguity in terminology and concepts of the domain, alignment to subdomains and business capabilities, team organization for autonomy and physical location, legacy code base, third party integration and a host of other factors.

## Why Teams Need To Realign With DDD’s First Principles

As you will have noticed, the majority of effort when applying the practices of Domain-Driven Design lie outside of the technical realm. Many people’s first introduction with Domain-Driven Design is an exposure to the tactical design patterns as well as techniques such as event sourcing or CQRS. They never experience or learn to appreciate the true power of DDD because they aren’t aware or don’t focus on the non technical aspect of software creation. It is the deep understanding of the problem space and the relentless focus on the core domain that allow effective and collaborative model-driven designs to lead to a viable solution. Only then do we need to leverage tactical patterns to organise code in such a manner as to reduce accidental complexity.

### Why Domain-Driven Solutions Often Fail To Deliver 

The reason that solutions fail to deliver, and the reason we need to focus on first principles, is not because of a lack of programming ability or technical expertise, but rather because of a lack of understanding, communication, and business knowledge. I am not saying technical people are lazy just that output doesn’t always translate to outcome. This lack of understanding stems from how developers capture knowledge of the problem domain they work in. Put another way, if developers and customers cannot effectively communicate, aren’t aligned on the same overarching goals then even with the most accomplished programmers in the world, you ultimately cannot produce meaningful outcomes. 

Having the right soft skills to avoid becoming entrenched or attached to an early version of a model is also important. For example having a technically supple model is great, but useless if you're not able to realise it doesn’t work as your initial understanding was proved to be incorrect.

#### Striving For Tactical Pattern Perfection

Teams concerned only with writing code focus on the tactical patterns of DDD. They treat the building block patterns as a bible rather than a guide, with no understanding of when it’s okay to break the rules. They waste effort adhering to the rules of the patterns. This energy is better spent on understanding why it needs to be written in the first place. DDD is about discovering what you need to write, why you need to write it, and how much effort you should use. The tactical patterns of DDD are the elements that have evolved the most since Eric’s book was written, with the strategic side of DDD remaining faithful to Eric Evan’s original text, albeit there has been great progress on the techniques of how to distill problem spaces which I will discuss later. How development teams create domain models is not nearly as important as understanding what models to write in the first place and how to develop them in a bounded context. Understanding the what and the why of problem solving is a more important process to get correct than how you are going to implement it in code.

#### Over Valuing Sample Applications

One of the most often-asked questions on software development forums is “Can I see a sample application?” There are probably many good solutions that show the result of a product developed under a DDD process, but much of the benefit of DDD is not revealed when you only examine the code artifacts. DDD is performed on whiteboards, over coffee, and in the corridors with business experts; it manifests itself when a handful of small refactorings suddenly reveal a hidden domain concept that provides the key to deeper insight. A sample application does not reveal the many conversations and collaborations between domain experts and the development team nor does it reveal the “Aha!” moments when deeper understanding of the problem domain is discovered.

The code artifact is the product of months and months of hard work, but it only represents the last iteration. The code itself would have been through a number of guises before it reached what it resembles today. Over time, the code will continue to evolve to support the changing business needs; a model that is useful today may look vastly different to the model used in future iterations of the product.

If you were to view a solution that had been built following a DDD approach hoping to emulate the philosophy, a lot of the principles and practices would not be experienced, and too much emphasis would be placed on the building blocks of the code. Indeed, if you were not familiar with the domain, you would not find the underlying domain model very expressive at all.

#### Missing The Real Value Of DDD

A team focusing too much on the tactical patterns is missing the point of DDD. The true value of DDD lies in the creation of a shared language, specific to a context that enables developers and domain experts to collaborate on solutions effectively. Code is a by-product of this collaboration. The removal of ambiguity in conversations and effortless communication is the goal. These foundations must be in place before any coding takes place to give teams the best chance of solving problems. Problems are solved not only in code but through collaboration, communication, and exploration with domain experts. Developers should not be judged on how quickly they can churn out code; they must be judged on how they solve problems with or without code.

### Going Back To First Principles

The first principles emphasise that focus for technical teams should be more aligned with the domain and driving all decisions from that position rather than only on technical concerns. After all with DDD the clue is in the name, the domain is the business, drive all design decisions based on the specifiction “will this help me achieve the business goal?”. If you don’t have a solid understanding of the goal then it is unlikely you will make good decisions. All decisions need to be taken in the wider context of your business and how what you do enables value to be produced.

In the remainder of this essay I will present to you each of these five first principles that I have distilled down from the non-technical aspects of DDD and learned to focus on during my career to allow me to really use the power of DDD.

My first principles are:

 1. Gain agreement on the problem
  * Focusing on the motivation behind the need for a solution and understanding the problem within the wider context of the business.
  * Contributing to delivering real business value by empathising with your business colleagues regarding the opportunity you are enabling or the constraint you are removing.

 2. Collaborate towards a solution
  * Moving past requirements gathering through collaborating on the vision and direction of a solution and the impacts that will resolve the problem. 
  * Gaining alignment by investing time and energy at the core problem sub domain.

 3. Ensure the solution solves the core problem
  * Focusing on outcomes over output to prevent over complex code and unnecessary investment. 
  * Avoiding becoming attached to a solution by keeping things simple and being comfortable that you never know as much as you think you do.

 4. Optimize the overall system
  * Having shared accountability for the entire system/process over siloed team optimisation.
  * Aligning on the big picture goal and understanding how you contribute.

 5. Be a positive influence on the team 
  * Being respectful, having patience and showing passion.
  * Displaying humility and empathy with others whilst reaching solutions as a team.

I would hasten to add that however well you manage the non technical side, it goes without saying you need to have a proficient technical ability. However I have often witnessed that a good understanding of the goal of the core domain and the problem space itself enables a simpler solution to be found that requires a simpler technical implementation.


## Principle 1: Gain Agreement On The Problem

 > “If you do not deal directly with the core problem, don’t expect significant improvement.” —Eli Goldratt
 
To know where to focus effort you first need to understand the motivation for solving a problem. You need to have a solid understanding of the business big picture so that you are able to understand a problem in context. What problems, constraints, opportunities exist that have led up to this point and proved that this problem deserves a solution? 

Why you ask? The reason is to ensure you truly understand what you are being tasked with to solve. As without this fundamental information it is impossible to be certain that you will be able to produce a solution with significant and beneficial outcomes. I will let you in on a secret - your business counterparts don’t have all the answers. They are experts in their respective domains, as you are in your technical domain. But they are not system or process design experts. They are hypothesising on what they should do. Therefore instead of taking things at face value, collaborate and empathise so you can see the thought processes of your business counterparts and understand how they arrived at their conclusions. This activity often leads to a technical team being able to add real value by looking at simpler alternative solutions or problems further up the supply/process chain that may have been missed. Techniques such as impact mapping are great for highlighting this.

![Understand the problem domain in contetx of the wider business](images/scott-millett/agreement_on_the_problem.png)

It is always worth asking why rather than just accepting that someone else has ensured that this is the correct solution to the business need further up the chain and not simply a local optimisation or a wish list item. How will building an application make a difference to the business? How does it fit within the strategy of the company? Why are we looking at technical solution? Does part of the software give the business a competitive edge? Often the result of systematically asking "why" will reveal a painfully simple solution or a complete change in direction. Clearly, don’t ask the question as a child might; be creative with how you search for the truth, but pull on the string of a problem until you reach the root of the matter.

Of course I am not expecting you to be a proxy CEO and change the direction of a company. But you ought to at least question and understand people's motivation for problem solving at a deeper level. This will enable you, and your team, to buy in and be fully committed to an idea.

### Be Clear On How You Deliver Business Value

 > “People don't want to buy a quarter-inch drill, they want a quarter-inch hole.” Theodore Levitt

A software developer is primarily a problem solver. Their job is to remove blockers that prevent the business producing value rather than producing code. Code should be viewed as the by product of finding a solution to a business problem, meaning that, on occasion, developers can actually solve problems without having a technical solution at all. Focus should be squarely on contributing to business outcomes over software output. It’s not about writing elegant code, it’s about getting results that benefit the business and help achieve its goal.

The IT department is part of the business, you should strive beyond creating software based on what you understand from the business to creating solutions that contribute to the overall business goal. This is a small but important distinction. Its similar to the paradoxical saying “I’m stuck in traffic” - you are not stuck in traffic, you are traffic. Software developers ARE the business, they just happen to be domain experts in software design just as accountants are domain exports in finance. You should not have a them and us mentality. 

As I have already mentioned, IT is far more strategic in most businesses than ever before. The advances in technology have disrupted many markets, think of Kodak and Blockbuster, giants businesses that have vanished. Delivering true value stems from acting from a domain perspective and identifying opportunities through leveraging your technical domain knowledge to help your business counterparts understand the art of the possible. Look for the money, how can I help shift the KPI, how can I contribute to removing a  bottleneck to business throughput? This is how you win, this is how you deliver real value.

### Techniques For Revealing Where Business Value Lies
There are a plethora of techniques to extract where you should focus to enable business value. Such as 

 * The Business Model Canvas
 * The Lean Enterprise Innovation Portfolio
 * Wardley Mapping
 * Customer Journey Mapping
 * Domain Storytelling

I will explain the four practices that I have found particularly useful and powerful to me.

#### Event Storming

Event Storming is a workshop activity that is designed to quickly build an understanding of a problem domain in a fun and engaging way for the business and development teams. Groups of domain experts, the ones with the answers, and development team members, the ones with the questions, work together to build a shared understanding of the problem domain. 

Knowledge crunching occurs in an open environment that has plenty of space for visual modeling, be that lots of whiteboards or an endless roll of brown paper.
The problem domain is explored by starting with a domain event; i.e., events that occur within the problem domain that the business cares about. A Post-it note representing the domain event is added to the drawing surface and then attention is given to the trigger of that event. An event could be caused by a user action that is captured and added to the surface as a command. An external system or another event could be the originator of the event; these are also added to the canvas. This activity continues until there are no more questions. The team can then start to build a model around the decision points that are made about events and when they, in turn, produce new events.

Event storming is an extremely useful activity for cultivating a UL as each event and command is explicitly named, this goes a long way to producing a shared understanding between the developers and business experts. The biggest benet however is that it’s fun, engaging, and can be done quickly. Alberto Brandolini created this activity and more information can be found at [eventstorming.com](https://www.eventstorming.com).


#### Impact Mapping

A technique for better understanding how you can influence business outcomes is impact mapping. With impact mapping, you go beyond a traditional requirements document and instead you try to work out what impacts the business is trying to make. Do they want to increase sales? Is their goal to increase market share? Do they want to enter a new market? Maybe they want to increase engagement to create more loyal customers who have a higher lifetime value.

Once you understand the impact the business is trying to make you can play a more effective role in helping them to achieve it. Significantly for DDD, you will be able to ask better questions during knowledge-crunching sessions since you know what the business wants to achieve. Surprisingly, impact mapping is a very informal technique. You simply create mind‐map-like diagrams that accentuate key business information. You work with the business so that, like knowledge crunching, it is a collaborative exercise that helps to build up a shared vision for the product. 

An impact map, rather obviously, starts with the impact. For example “sell 25% more bicycles”. Directly connected to the impact are the actors—the people who can contribute to making the desired impact. That would be developers and data scientists. Child nodes of the actors are the ways in which the actors can help. One way the developers can help to create the business impact is to improve the performance of the website so that people are more likely to make a purchase. Finally, the last level of the hierarchy shows the actual tasks that can be carried out. You can see in the image that one way the developers may be able to make the website faster is to remove slow frameworks.

![Impact Mapping](images/scott-millett/Impact-Map.png)

On many software projects the developers only get the lower tiers of an impact map—what the business thinks they need and how they think the developers should achieve it. With an impact map, though, you can unwind their assumptions and nd out what they really want to achieve. And then you can use your technical expertise to suggest superior alternatives that they would never have thought of.

Some DDD practitioners rate impact mapping very highly, both when applied with DDD or in isolation. You are highly encouraged to investigate impact mapping by browsing the website (http:// www.impactmapping.org/) or picking up a copy of the book: “Impact Mapping,” by Gojko Adzic.

#### Understanding The Business Model

A business model contains lots of useful domain information and accentuates the fundamental goals of a business. Unfortunately, very few developers take the time to understand the business model of their employers or even to understand what business models really are.

One of the best ways to learn about a company’s business model is to visualize it using a Business Model Canvas; a visualization technique introduced by Alexander Osterwalder and Yves Pigneur in their influential book, “Business Model Generation” is highly recommended and very accessible reading for developers. A Business Model Canvas is extremely useful because it breaks down a business model into nine building blocks, as shown in image, which illustrates an example Business Model Canvas for an online sports equipment provider.

![Business Model Canvas](images/scott-millett/Business-Model-Canvas.png)

Understanding the nine building blocks of a business model tells you what is important to the business. Key information like: how it makes money, what its most important assets are, and crucially its target customers. Each of the sections of a business model is introduced below. For more information, the “Business Model Generation” book is the ideal learning resource.

 * Customer Segments—the different types of customers a business targets. Examples include niche markets, mass markets, and business‐to‐business (b2b).
 * Value Propositions—the products or services a business offers to its customers. Examples include physical goods and cloud hosting.
 * Channels—how the business delivers its products or services to customers. Examples include physical shipping and a website.
 * Customer Relationships—the types of relationships the business has with each customer segment. Examples include direct personal assistance and automated electronic help facilities.
 * Revenue Streams—the different ways the business makes money. Examples include advertising revenue and recurring subscription fees.
 * Key Resources—a business’s most important assets. Examples include intellectual property and important employees.
 * Key Activities—the activities fundamental to making the business work. Examples include developing software and analyzing data.
 * Key Partnerships—a list of the business’s most significant partners. Examples include suppliers and consultants.
 * Cost Structure—the costs that the business incurs. Examples include salaries, software subscriptions, and inventory.

Armed with the information presented by a Business Model Canvas you will be empowered to ask meaningful questions of domain experts and help to drive the evolution of the business—not just the technical implementation. The small effort of finding and understanding your employer’s business model is well worth it.

 
#### Applying The Theory Of Constraints And Systems Thinking

The theory of constraints (TOC) is a management paradigm introduced by Eli Goldratt that states that a system will be limited to achieving its goals by a few small constraints. Therefore focus and effort should be aimed at removing these constraints to the system above anything else. This will ensure that any output of effort results in maximum outcome to the business goal - more often than not gaining money. In very simple terms, identify the bottleneck that restricts the production of business value and remove.

TOC has a five step process:

 * Identify the constraint. 
   Understand the key issue that is causing a bottleneck or preventing your business generating value 

 * Determine how to eliminate the constraint. 
   Focus all efforts at removing the constraint as fast as possible

 * Subordinate everything else to the constraint. 
   Don’t be distracted by any other problems that are not contributing the constraint. Any other effort elsewhere is wasted effort. The constraint is the priority to resolve.

 * Remove the constraint. 
   Apply the solution to the constraint in order to remove it.

 * Determine if the constraint has been removed.
   Sometimes you can push a problem down or up stream. If this is the case simply repeat the steps for the new constraint.

TOC is all about macro level over micro level thinking. It's not about optimising the link, its about optimising the entire chain or the system. To put into other words it's about optimizing your business to achieve its goals rather than a sub-department of service.

Why is this relevant to DDD you may ask? DDD has the domain or business at the heart of its philosophy, in that design decisions should be about driving business value. If you don't understand the constraint that is stopping the business from producing value then you can’t make a good decision on where to focus effort. The constraint could be your core domain or it could be a problem in a supporting domain that affects your core domain. Improving anything other than the constraint may have value but it won't be the most valuable thing to do. It's about removing silo mentally and making sure that teams understand the bigger picture so that they can apply effort in the best possible place. 

As an example, imagine you are part of a team that has been tasked with increasing online transactions by 10%. In order to gain alignment on where to focus you could apply TOC to determine what is the constraint for people checking out. Is it the registration page? If you see a high amount of dropouts you could look for a solution and correct the problem. Then you would look to see what the next big constraint to checking out is. It could be that the checkout flow is fine but by actually increasing the range of products available you would achieve 10% increase in transactions, all being equal.Alternatively if you optimised payment it would have little impact, even if done with great effort and skill, as the constraint is further up the flow. 

## Principle 2: Collaborate Towards A Solution

By gaining alignment on the real business constraint or opportunity you will be able to progress from having a shallow understanding of your problem domain but a good grasp on requirements to a deep understanding of business needs with an eye on opportunities that you can enable. Remember, people will tell you what they want rather than what is needed, the difference is subtle but leads to very different outcomes. Therefore don’t sit and wait for requirements - offer solutions. 

Start with a big picture understanding of the vision of the solution so that everyone has an alignment point. Highlight the important areas and those that need only to be good enough. Facilitate collaborative workshops on model design and problem simplification. You need to actively participate in solution design away from the computer. Contribute to your own requirements, don’t leave it to others.

I often wonder if the titles of roles are somewhat self fulfilling. When I first started out in the world of IT my first job title was Analyst Programmer. The definition of an analyst is an individual who performs analysis of a topic and Programmer is a person who writes computer programs. Therefore half of my job was to understand about problems and the other half was to translate that understanding into language a computer could understand. Titles such as software developer and engineer focus solely on the technical side and assume that the solution is refined enough that it can be turned into a set of requirements. The reality as we all know is seldom so.

A focus purely on the technical side highlights a bigger problem: when designing software for systems with complex logic, typing code will never become a bottleneck. The code is an artifact of developers and domain experts working together and modeling the a solution for the problem domain. The code represents the end of the process of that collaboration and discovery. A developer’s job is to problem solve, and problem solving is sometimes easier done away from the keyboard in collaboration with domain experts. In the end, working code is ultimately the result of learning and an understanding of the domain.


### Show Passion For The Problem Domain

 > “Ignorance  is  the single  greatest  impediment  to  throughput.” Dan North

Developers are fantastic at educating themselves on technology and project methodologies; however, decomposing a problem and being able to distill what is important from what is not will enable a good developer to become a great one. Ensure you spend as much time working to understand the problem space as you do in the solution space.

Just as a useful model is derived over a series of iterations, so too must a problem space be refined to reveal the true intent behind the original vision. Listening and drawing the why as well as the what and when from stakeholders is a skill that developers should practice just as they practice coding katas.

Software development is a learning process, so is the quest to reveal deep insights in your problem domain. Software development is about understanding; software that works to solve a business problem proves that understanding. Curiosity and a genuine desire to learn about a problem space is vital to produce good solutions and meaningful software. If you want to be good at anything, you need to practice, practice, practice. If you want to be a great developer rather than a good one, you need to show passion for the problem and commit to understand your domain. 

To apply the principles of DDD, you need a driven and committed team—a team committed to learning about its craft and the problem domains it works in. Passion lies within all of us, and if you feel value in the practices of DDD, it is up to you to inspire your team and become an evangelist. Passion is contagious; if you commit to spend time with your domain experts to understand at a deeper level and can show how this results in a more expressive codebase then your team will follow.

Have passion for the problem space, Be proactive, be curious - this will make it easier to find solutions and more importantly opportunities. You cannot begin to be useful to solve a problem or look for opportunity if you don't really understand the domain you are working in to a sufficiently deep level. You are a professional. You are paid well. You have a responsibility to understand the domain you are in.

### Learn To Facilitate Solution Exploration

Making sense of a complex problem domain in order to create a simple and useful model requires in-depth knowledge and deep insight that can only be gained through constant collaboration with the people that understand the domain inside and out. Complex problem domains will contain a wealth of information, some of which will not be applicable to solving the problem at hand and will only act to distract from the real focus of your modelling efforts. Knowledge crunching is the art of distilling relevant information from the problem domain in order to build a useful model.

Domain knowledge is key, even more so than technical know‐how. Teams working in a business with complex processes and logic need to immerse themselves in the problem domain and, like a sponge, absorb all the relevant domain knowledge. This insight will enable teams to focus on the salient points and create a model at the heart of their application’s code base that can fulfill the business use cases and keep doing so over the lifetime of the application.

Facilitation skills are vital in order to efficiently and effectively distill knowledge from domain experts. You don’t need to be the smartest person but you do need to be able to collaborate and facilitate with smart people to gain deep insights. Only by asking the right questions can decisions be made, knowledge can be shared and a solution can be revealed and agreed upon. As covered in the Principle 1: Gain Agreement on the Problem Alberto Brandolini has done a tremendous amount of work in this area under the practice of event storming and big picture visual modeling. But this can also be used to focus on solution exploration at a lower level.

The key to facilitation is about guiding people not to an answer but to a shared understanding and empowering them to take responsibility. It’s not to lead a group and make good decisions, it is to make sure good decisions get made. Workshops and collaborative working must enable a platform that accepts different points of views. No one should have the authority on a good idea, and no suggestion is stupid
 
### Deliberate Discovery At The Constraint

Dan  North, the  creator  of  BDD, has  published  a  method  for  improving domain  knowledge  called  deliberate  discovery.  Instead  of  focusing  on the  framework  of  agile  methodologies  during  planning  and  requirement gathering  stages, such  as  the  activities  of  planning  poker  and  story creation, you  should  devote  time  to  learning  about  areas  of  the  problem domain  that  you  are  ignorant  about.  A  greater  amount of  domain  knowledge  will  improve  your  modeling  efforts. At  the  start  of a  project  teams  should  make  a  concerted  effort  to  identify  areas  of  the problem  domain  that  they  are  most  ignorant  of  to  ensure  that  these  are tackled  during  knowledge-crunching  sessions. Teams  should  use knowledge-crunching  sessions  to  identify  the  unknown  unknowns, The parts  of  the  domain  that  they  have  not  yet  discovered. This  should  be  led by  the  domain  experts  and stakeholder  who  can  help  the  teams  focus  on areas  of  importance, such as an identified constraint or bottleneck,  and  not  simply  crunching  the  entire  problem domain. This  will  enable  teams  to  identify  the  gaps  in  domain  knowledge and  deal with  them  in  a  rapid  manner.


### Don’t Ask For Requirements, Look For Impact Opportunities 

 > “Opinion is really the lowest form of human knowledge. It requires no accountability, no understanding. The highest form of knowledge… is empathy, for it requires us to suspend our egos and live in another’s world. It requires profound purpose larger than the self kind of understanding.” ― Bill Bullard

Be wary of business users asking for enhancements to existing software, because they will often give you requirements that are based on the constraints of the current systems rather than what they really desire. Ask yourself how often you have engaged with a user to really understand the motivation behind a requirement. Have you understood the why behind the what? Once you share and understand the real needs of a customer, you can often present a better solution. Customers are usually surprised when you engage them like this, quickly followed by the classic line: “Oh, really? I didn’t know you could do that!” Remember: You are the enabler. Don’t blindly follow the user’s requirements. Business users may not be able to write effective features or effectively express goals. You must share and understand the underlying vision and be aware of what the business is trying to achieve so you can offer real business value.

Requirements assume someone has all the answers - this is a massive fallacy. We have progressed passed the stage of simply getting requirements from people. We now should be able to partner with business counterparts in order to remove problems or introduce them to the art of the possible and the endless opportunities technology can enable. Remember be accountable, don't be lazy - don’t delegate solution design to the business. It’s not someone else’s problem, it’s yours. Domain experts are not system experts. Learn and discover with them. I have often found it the case that domain experts don’t necessarily know how current system works, or should work. They are domain experts, experts in their fields, but not business process engineers, not systems experts.

### Focus On The Most Interesting Parts

 > “There is no compression algorithm for experience” -Andy Jassy, CEO AWS

The collaboration between the business and the development team is an essential aspect of DDD and one that is crucial to the success of a product under development. However, it is important to seek out those who are subject matter experts in the domain you are working in and who can offer you deeper insight into the problem area. DDD refers to these subject matter experts as domain experts. The domain experts are the people who deeply understand the business domain from its policies and workows, to its nuisances and idiosyncrasies. They are the experts within the business of the domain; they will rarely, if ever, have the title of domain expert. Instead, look for the product owners, users, and anyone who has a great grasp and understanding for the domain you are working in regardless of title.

When picking scenarios to model, don’t go for the low-hanging fruit; ignore the simple management of data. Instead, go for the hard parts—the interesting areas deep within the core domain. The opposite of this is bikeshedding - which is the art of spending a disproportionate amount of time and energy over an insignificant or unimportant detail of a larger problem. The term comes from a story of a meeting to discuss the development of a nuclear power plant in which the majority of the time is spent on the design of the bike shed as that is the only part that everyone is able to understand.

Therefore focus on the parts of the product that make it unique; these will be hard or may need clarification. Time spent in this area will be well served, and this is exactly why collaboration with domain experts is so effective. Using domain experts’ time to discuss simple create, read, update, and delete (CRUD) operations will soon become boring, and the domain expert will quickly lose interest and time for you. Modeling in the complicated areas that are at the heart of the product is exactly what the principles of DDD were made for.

#### The Core Focus of PotterMore.com

Pottermore.com was the only place on the web where you can buy digital copies of the Harry Potter books. Like any e‐commerce site, it allows you to browse products, store products in a basket, and check out. The core domain of the Pottermore site
is not what the customer sees, but rather what he does not. Pottermore books aren’t DRM‐locked (http://www.futurebook.net/content/pottermore-finally- delivers-harry-potter-e-books-arrive); they are watermarked. This invisible watermark allows the books that are purchased to be tracked in case they’re hosted illegally on the web. The core domain of the Pottermore system is the subdomain that enables this watermarking technology to deter illegal distribution of a book without infringing on the customer. (The customer can copy the book to any other of his devices.) This is what was most important to the business, what set it apart from other e‐book sellers, and what ensured the system was built rather than being sold on iTunes or other e‐book sellers.

### Ensure Everyone Understands The Vision Of The Solution

A domain vision statement can be created at the start of a project to explicitly capture what is central to the success of the software, what the business goal is, and where the value is. This message should be shared with the team and even stuck up on a wall in the office as a reminder to why the software is being written.

#### Amazon’s Approach To Product Development 

Amazon has a unique approach when it comes to forming a domain vision statement called working backwards (see: http://www.quora.com/What-is- Amazons-approach-to-product-development-and-product-management).
For new enhancements, a product manager produces an internal press release announcing the finished product, listing the benefits the feature brings. If the intended customer doesn’t feel the benefits are exciting or worthwhile, the product manager refactors the press release until the feature offers real value for the customer. At all times, Amazon is focused on the customer and is clear about the advantage a new feature can bring before it sets out with development.


## Principle 3: Ensure The Solution Solves The Core Problem

 > “Technology can bring benefits if, and only if, it diminishes a limitation.”, Eli Goldratt

An initial model is a product of exploration and creativity. However you should not stop at the first useful model you produce and you should constantly validate your model against different ideas and new problems. Experimentation and exploration fuel learning and vital breakthroughs only occur when teams are given time to explore a model and experiment with its design. Spending time prototyping and experimenting can go a long way in helping you shape a better design. It can also reveal what a poor design looks like. You need to challenge your assumptions and realign with the big picture. Ask yourself are you sure that you are focused on the core problem and have not been distracted by an interesting yet less valuable side problem? Is the solution cost effective and simple enough? If the solution is complex have we missed a chance to simplify the problem? 

### Focus Effort On Outcome Over Output

In an ideal world, quality software would always be top of your agenda; however, it’s important to be pragmatic. Sometimes a new system’s core domain could be first to market, or sometimes a business may not be able to tell if a particular idea will be successful and become core to its success. In this instance, the business wants to learn quickly and fail fast without putting in a lot of up-front effort.

The first version of a product that is not well understood need not be well crafted. There may be uncertainty if the endeavour will be invested in over time, and therefore you need to understand why speed of delivery could top initial supple design. However, if the product is a success and there is value in a prolonged investment in the software, you need to refactor to support the evolution; otherwise, the technical debt racked up in the rush to deliver starts to become an issue. It’s a balancing act to produce code that will help you in the future against getting product out in front of customers for fast feedback.

#### Strive For Simple Boring Code

 > “Simplicity is prerequisite for reliability.”, Edsger W. Dijkstra

Teams that are aligned with the philosophy of DDD focus more on the bigger picture and understand where to put the most effort. They will not apply the same architecture to all parts of a solution, and they will not strive for perfection in areas of little value. They will trade isolated and working software for unnecessary elegance and gold plating.
Only the core domains need to be elegant due to complexity or importance. This is not to say that all other code should be poorly written, but sometimes good is good enough.

Applying techniques designed to manage complex problems to domains with little or no complexity will result in at best wasted effort and at worst needlessly complicated solutions that are difficult to maintain due to the multiple layers of abstractions. DDD is best used for strategically important applications; otherwise, the deep knowledge gained during DDD provides little value to the organization.

When creating a system, developers should strive for simplicity and clarity. Software that is full of abstractions achieves little more than satisfying developers’ egos and obscuring the reality of a simple codebase. Developers who aren’t engaged with delivering value and are instead only focused on technical endeavors will invent complexity because they’re bored by the business problem. This kind of software design can lead to frustration for teams in the future that need to maintain the mess of technical layers.

Don’t let design patterns and principles get in the way of getting things done and providing value to the business. Patterns and principles are guides for you to produce supple designs. Badges of honor will not be given out the more you use them in an application. DDD is about providing value, not producing elegant code.

Keep your model simple and focused, and strive for boring plain code. Often teams quickly fall into the trap of overcomplicating a problem. Keeping a solution simple does not mean opting for the quick and dirty; it’s about avoiding mess and unnecessary complexity. Use simplicity during code review or pair programming. Developers should challenge each other to ensure they are proving a simple solution and that the solution is explicitly focused only on the problem at hand, not just a general solution to a generalized problem.


#### The Jurassic Park Principle

 > "Your scientists were so preoccupied with whether or not they could that they didn't stop to think if they should.” Dr. Ian Malcom, Jurrasic Park

All problems are not created equal; some are complex and are of little business value, so it makes no sense to waste effort in finding automated solutions for them. Complex edge cases do not always need automated solutions. Humans can manage by exception. If a problem is complex and forms an edge case, speak to your stakeholder and domain expert about the value of automating it. Your effort could be better served elsewhere, and a human might better handle this exception. You can produce elegant and beautiful software but if it provides no value or misses the point then it is utterly useless. 

Simple problems require simple solutions. Trivial domains or subdomains that do not hold a strategic advantage for businesses will not benefit from all the principles of DDD. Developers who are keen to apply the principles of DDD to any project regardless of the complexity of the problem domain will likely be met with frustrated business colleagues who are not concerned with the less important areas of a business. Talk to people about the opportunity cost before writing code and don’t worry about not solving all the problems.

If we remind ourselves of the theory of constraints we should avoid local optimisations at expense of improving the system. You should ask yourself will your output produce meaningful outcomes - should you expend lots of effort and energy on are area of the solution that does not impact the core domain?

You need to master the art of saying no. This is of course very difficult in practice, but it is worth it. Well meaning business counterparts may want you to optimise for their department at the expense of the system. Empathising with them and helping them understand how this distracts you from the overall goal will give you more time to focus on the strategic high value areas. 


#### Build Subdomains For Replacement Rather Than Reuse

When developing models in subdomains try and build them in isolation with replacement in mind. Keep them separated from other models, legacy code, and third party services by using clean boundaries. By coding for replacement rather than reuse you can create good enough supporting subdomains without wasting effort on perfecting them. In the future they can be replaced by off‐the‐shelf solutions or can be rewritten as business needs change. Stiive for good boundaries rather than perfect models. Boundaries are often harder to change than a model.


#### Simplify The Solution By Simplifying The Problem

Writing software is costly, code is expensive to produce and maintain. If you can solve a solution without code it’s great. If you can limit what you output this is a good thing. Teams should be rewarded for developing simple solutions that enable business capability at a low actual cost and low opportunity cost. One way to do this is to change the problem. If you have a poorly understood or inefficient business process then applying a technical solution to it will simply create an expensive automated, but more complex process.

Don’t be lazy and code around the problem. Sometime it’s easier to code and add to domain complexity rather than change business process as it’s difficult to get the decision makers in a room. But you must do everything you can to simplify problems so that you can produce simpler solution models. Highlight overly verbose or poor business process to your business counterparts so that are able to make changes. It’s easy and lazy to not change process with the excuse that it’s been like that and it’s established, especially when it requires complex code to work around it. We understand the value of code refactoring why not refactor the business? Don’t accept mediocrity in business process, highlight it at the root and speak to your business counterparts before trying to automate.

### Challenge Your Solution

 > "All good solutions have one thing in common: they are obvious but only in hindsight.", Eli Goldratt

When you are starting out on a new solution you are probably least knowledgeable about the domain. Paradoxically this is also the time when you will be making important decisions. Complex domains are full of uncertainty, you need to be comfortable with this and with not knowing all the answers upfront. Remember a wrong choice is rather like an AB test, you chalk it up to experience and you have more knowledge on what doesn’t work.

They say all models are wrong, its just that some are more useful. Your initial model will be wrong, but don’t get too hung up. Remember you need to love the problem not your initial solution. The process of learning more about the problem domain is achieved over many iterations and evolutions.. Your knowledge will grow, and to your solution, into something useful and appropriate.

Explore and experiment to reveal insights and offer new solutions. The result of tackling a problem from various angles is not the creation of a perfect model but instead the learning and discovery of concepts in the problem domain. This is far more valuable and leads to a team able to produce a useful model at each iteration.

#### Model Exploration Whirlpool


Eric Evans has created a draft document named the Model Exploration Whirlpool (http://domainlanguage.com/ddd/whirlpool/). This document presents a method of modeling and knowledge crunching that can complement other agile methodologies and be called upon at any time of need throughout the lifetime of application development. It is used not as a modeling methodology but rather for when problems are encountered during the creation of a model. Telltale signs such as breakdowns in communication with the business and overly complex solution designs or when there is a complete lack of domain knowledge are catalysts to jump into the process dened in the Model Exploration Whirlpool and crunch domain knowledge.


The whirlpool contains the following activities:

 * Scenario Exploring
A domain expert describes a scenario that the team is worried about or having difficulty with in the problem domain. A scenario is a sequence of steps or processes that is important to the domain expert, is core to the application, and that is within the scope of the project. Once the domain expert has explained the scenario using concrete examples the team understands, the group then maps the scenario, like event storming in a visual manner in an open space.

 * Modeling
At the same time of running through a scenario, the team starts to examine the current model and assesses its usefulness for solving the scenario expressed by the domain expert.

 * Challenging the Model
Once the team has amended the model or created a new model they then challenge it with further scenarios from the domain expert to prove its usefulness.

 * Harvesting and Documenting
Significant scenarios that help demonstrate the model should be captured in documentation. Key scenarios will form the reference scenarios, which will demonstrate how the model solves key problems within the problem domain. Business scenarios will change less often than the model so it is useful to have a collection of important ones as a reference for whenever you are changing the model. However, don’t try and capture every design decision and every model; some ideas should be left at the drawing board.

 * Code Probing
When insight into the problem domain is unlocked and a design breakthrough occurs the technical team should prove it in code to ensure that it can be implemented.

#### Exploring Multiple Models

> "It's better to be approximately right than precisely wrong." —Eli Goldratt

Most teams usually stop exploring and jump to their keyboards when they arrive at the first useful model. Your first model will unlikely be your best. Once you have a good model, you should park it and explore the problem from a different direction. It’s not about being right or wrong it’s about moving forward, progressing and driving toward value. You will make wrong decisions but only from the luxury of hindsight so please don’t beat yourself up - remember this is a learning process.

There is no such thing as a stupid question or a stupid idea. Wrong models help to validate useful ones, and the process of creating them aids learning. When working in a complex or core area of a product, teams must be prepared to look at things in a different way, take risks, and not be afraid of turning problems on their head. For a complex core domain, a team should produce at least three models to give itself a chance at producing something useful. Teams that are not failing often enough and that are not producing many ideas are probably not trying hard enough. When deep in conversation with a domain expert, a team should not stop brainstorming at the first sign of something useful. Once the team gets to a good place, it should wipe the whiteboard and start again from a different angle and try the what-if route of investigation. When a team is in the zone with an expert, it should stay there until it exhausts all its ideas.

Only stop modelling when you have run out of ideas and not when you get the first good idea. Once you have a useful model start again. Challenge yourself to create a model in a different way, experiment with your thinking and design skills. Try to solve the problem with a completely different model. Constantly refactor to your understanding of the problem domain to produce a more expressive model. Models will change with more knowledge. Remember a model is only useful for a moment in time; don’t get attached to elegant designs. Rip up parts of your model that are no longer useful, and be willing to change when new use cases and scenarios are thrown at your design.
 

## Principle 4: Optimize the Overall System

 > "A system is never the sum of its parts. It is the product of the interactions of its parts", Russel Ackoff 

When working on the solution to a problem teams must still keep an eye on the bigger picture. It is easy to become lost and distracted when you are in the detail and lose sight of what the goal is. We need to ensure that all parts of the decomposed solution are working for the greater good in a effective collaborative manner.

In large and complex domains, multiple models in context collaborate to fulfill the requirements and behaviors of a system or process. A single team may not own all of the various sub components of a system, some will be existing legacy code that is the responsibility of a different team, and other components will be provided by third parties that will have no knowledge of the clients that will consume its functionality. Teams that don’t have a good understanding of the different contexts within a system, and their relationships to one another, run the risk of compromising the models at play when integrating bounded contexts. Lines between models can become blurred resulting in a Big Ball of Mud if teams don’t explicitly map and understand relationships between contexts.

The technical details of contexts within systems are not the only force that can hamper the success of a solution. Organizational relationships between the teams that are responsible for contexts can also have a big impact on the outcome. Often, teams that manage other contexts are not motivated by the same forces, or they have different priorities. For solutions to succeed, teams usually need to manage changes in these situations at a political rather than technical level, or as Nick Tune refers to it - the sociotechnical design. 

What is important to understand is that it is not the individual components of a system that need to work, it is the system itself. Teams needs to learn to collaborate and agree to overcome any obstacles to implementation. To do this they must understand how they fit into to the system as a whole.

### Strive for team autonomy 

Multiple teams working together on a solution should be organised so that they are loosely coupled and as far as possible autonomous. Restricting the number of dependencies for a team will enable them to them to move faster. Ideally a team would also be aligned to a business capability (what the business does, rather than how it does it) that it is enabling and that contributes to the overall solution. In a perfect world the software team should be embedded in the business department that they are providing capability for rather than sit in a central IT org structure in order to develop a deeper understanding for their part of the domain.

Loosely coupled but highly cohesive teams can achieve autonomy if they understand the goal and have collaborated together on a solution. This causes alignment which enables autonomy. However be careful, without alignment loosely coupled teams can become silos and follow their own agenda and needs for their business department counterparts.

Boundaries are very important. Don’t rush for structure or put concrete boundaries in before you really understand your solution space. Try to avoid precision in the first instance as boundaries and organisational design are harder to move down the line. Play with the model and reveal the linguistic and business capability ownership boundaries before implementing software boundaries. Have patience, don’t force it or look for perfection, and don’t get hung up if you are proved wrong and need to rethink. It’s all valuable knowledge and experience. 

### Collaborate To Solve The Big Picture

 > “A company could put a top man at every position and be swallowed by a competitor with people only half as good, but who are working together.” W. Edwards Deming

Although having completely independent teams is a productivity win, it’s important to ensure that communication between teams still occurs for knowledge and skill‐sharing benefits. Ultimately, bounded contexts combine at run time to carry out full business processes, so teams need a big‐picture understanding of how their bounded context(s) fit into the wider system. Established patterns for this problem involve having regular sessions in which teams share with other development teams what they are working on, how they have implemented it, or any technologies that have helped them achieve their goals. Another excellent pattern is cross‐team pair programming. This involves moving a developer to a different team for a few days to learn about that part of the domain. You can spawn many novel approaches based on these two concepts of having group sessions and moving people around.

Collaboration is easier if you have alignment in what you are doing, this is why it's important to constantly align around the big picture so that everyone remembers the goal that they are separately contributing to. Context maps are important but not exclusive, process maps, event maps and event storming are ideal to visualise a shared understanding of system flow and ensure all teams are aligned by understanding the goal. 

There are a plethora of collaboration tools in any organisation. Slack, skype, email, phone are a few. However with a wash of collaboration tools I often find that teams have forgotten how to talk to each other. It is vital to have strong relationships with teams that you depend on. We must also ensure we take personal feelings out of how we work and attack the problem. Its ok to be angry, just be angry at the problem not the person. Complex systems will have many moving parts and many teams, after all no man is an island. People relationships are as important as code relationships, therefore refactor your personal relationships as they are key to delivering effective solutions.
  
### Identify Constraints In Delivering The Solution And Work Through Them

The context map, ever evolving, ensures that teams are informed of the holistic view of the system, both technical and organizational, enabling them to have the best possible chance of overcoming issues early and to avoid accidentally weakening the usefulness of the models by violating their integrity.

In complex systems there will be many dependencies. You should understand and work with others that own these dependencies to unblock flow for the big picture. The more you manage and, ideally, remove dependencies the easier your life will become.

In many ways, the communication between bounded contexts, both technical and organizational, is as important as the bounded contexts themselves. Information that context maps provide can enable teams to make important strategic decisions which improve the success of a solution. A context map is a powerful artifact that can bring new team members up to speed quickly and provide an early warning for potential trouble hot spots. Context maps can also reveal issues with communication and work within the business.

### Understanding Ownership And Responsibility

Accountability and responsibility are other non-technical areas that can affect the delivery of a solution. Defining team ownership and management for subsystems that you need to integrate with is essential for ensuring changes are made on time and in line with what you expect. Context mapping is about investigation and clarification; you may not be able to draw a clear context map straight away, but the process of clarifying responsibility, explicitly defining blurred lines, and understanding communication flow while mapping contexts is as important as the finished artifact.

When is comes to responsibility the entire team needs to understand what they are responsible for and how it fits in the bigger picture. Each member must have deep knowledge of what they are doing, why, and the logic behind the method being used to implement the solution. Of course, teams need to subscribe to the principle of what they build they support, but greater than this is the ability to clearly articulate how what they are building contributes to the system. Too often a team lead simply delegates components of a solution to junior members who have little or no idea how their part contributes to the whole.

### Identify The Grey Areas Of Business Process 

The business processes that happen between and take advantage of bounded contexts are often left in no‐man’s‐land without clear responsibility and clarity regarding their boundaries and integration methods. A context map, focusing on the nontechnical aspects of the relationships, can reveal broken business process flow and communication between systems and business capabilities that have degraded over time. This revelation is often more useful to the businesses that are able to better understand and improve process that spans across departments and capabilities. The insight can be used to identify the often gray area between contexts that govern business process and address the accountability void early to ensure that ownership is not simply assumed. These important orchestrational processes can often be devoid of responsibility from development teams and business ownership, but paradoxically are immensely important to business workflows and processes.

## Principle 5: Be A Positive Influence On The Team

 > “Complaining does not work as a strategy. We all have finite time and energy. Any time we spend whining is unlikely to help us achieve our goals. And it won't make us happier.” ― Randy Pausch, The Last Lecture

Domain-Driven Design isn’t a silver bullet. Just as switching from an upfront waterfall approach to a more agile/XP project methodology didn’t solve all your software development problems, opting to follow DDD won’t suddenly produce better software. The common denominator in any successful project is a team of clever people who are passionate about what they are doing and who care about it succeeding. As they say, culture eats strategy for breakfast.

However much time you will spend in front of the computer it will dwarf the time you spend working and talking to others. Show respect, patience and humility when working with your peers and business counterparts. Understand different personality types and how different types interact in collaborative sessions. Work out how people learn -  are they big picture people or detail people. Perfect the art of active listening and show empathy,  these are very important traits to get on in this world let alone in software development.

Teamwork and communication are as essential as technical ability in order to deliver change in large or complex domains. Enthusiasm and the ability to learn, technical and non-technical subject matter, are also key skills required by team members. These softer skills have as much, if not more to do with delivering success than technical knowledge alone. As I have mentioned before we have moved away from IT being an order taker that are simply given a dense set of requirements and told to get on with it. We need to empathise not only with business colleagues, but with business strategy and overarching needs. You don’t need rock stars, you need capable team players. 

In some respects coding is the easy part, after all, the computer will only do what you tell it to do (well most of the time). Collaborating with and understanding different people with different backgrounds and different ways of working is hard. You need to be able to play well with others. Problem solving is a team sport, getting or giving help is not a sign of weakness but is essential for improving oneself to become an effective team player.

Lastly don’t assume you know something, always be prepared to challenge your thinking and your opinions - you may be surprised on things you thought you knew. Do not be closed off to a new way of thinking or looking at problems from other people's point of views. Remember there is no right or wrong and it often has an awful lot to do with context.

## To The Next 15 Years And The Continued Reinvention Of DDD

DDD is now an uncontrollable force, it is far larger than the sum of its parts. It is a huge ever growing community of progressive and professional problem solvers learning how they can offer more to their business. I am afraid that even if we were to cut the head of off Eric Evans the community and practitioners would still grow and continue to evolve Domain-Driven Design. Plus he is a nice chap and it would make an awful lot of mess. 

In my opinion the future of DDD lies in the blending between non-technical and technical “business” people. Knowledgeable technical people will turn into business decision makers due to more focus on key underlying business problems. Those that embrace the business as much as they embrace technology will flourish as leaders and actively contribute to the  strategies of their domains rather than simply being order takers.

Thank you Eric for a fantastic book and thanks for the thousands that he has inspired (and that have inspired him). Thanks to those that have inspired me and given so much for the community to help us become a little better each day. Lastly remember it’s all about context so don't take what I say, or anyone says, verbatim, understand things and learn how to leverage the experience in your own context. Always be the humble student, don’t stop learning and never, never, never stop asking questions.


