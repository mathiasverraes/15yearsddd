# Tackling Complexity in ERP Software, a Love Song to Bounded Contexts (by Michiel Overeem)

Enterprise resource planning (ERP) software offers an integrated solution for the management of core business processes. Different domains (accounting, sales, relation management, payrolling) are handled by a single software system. A well-executed ERP system has the benefit that information is only stored once, and relations between information are easy to follow since it is all in one system.

We, AFAS Software in the Netherlands, have two decades of experience with building ERP software, and not without success. After working on the same codebase for so long, we strategically decided to do a rewrite. Yes, we know that Joel Spolsky said not to do that[^joel]. We are in the DHH-camp[^dhh], because the new version needs to be different. We needed to tackle the complexity in ERP software. Through our discovery of CQRS and event-sourcing we stumbled upon Domain-Driven Design (DDD). And the goal of DDD is to tackle the complexity in software, exactly what we needed. We let DDD inspire us as much as possible. But we also decided to take it a step further. We experienced three major challenges in developing ERP software that we wanted to tackle in this new version. 

[^joel]: <https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/>
[^dhh]: <https://signalvnoise.com/posts/3856-the-big-rewrite-revisited>

*Disclaimer: although we have quite a journey behind us, we have not arrived yet. The software is not yet in production, and our experiences come solely from testing the system in simulated environments.*

## The three challenges we faced

The first challenge is that ERP software has **a lot of repetitive logic**. There are numerous parts that look very similar. For instance, the maintenance of a product catalog is not that different from the maintenance of a list of organizations, from a technical point of view. In a large software system, if you are not careful, the two will be developed in isolation, and will work inconsistent. This inconsistency will bother end-users, because they have certain expectations of the usability of the system. Evolution of one of the maintenance components will also require extra work, because similar parts of the system need to be kept consistent. Obviously, ERP systems gain a lot from re-use and standards.

Developers can benefit a lot from reuse in ERP systems: it can increase productivity and quality. However, reuse can become a pain in the long run. Changing the library that is used in numerous places is hard and can result in unpredictable outcomes. New developers do not know the history of that library, and do not have the bigger picture to oversee their changes. Teams must be careful with reuse, while it looks temping in the beginning, refactorings can be very expensive. 

The second challenge is that ERP software requires **a high level of customizability**. Processes within businesses look similar, but when customers are spread out over different branches and all have their specific needs, the processes are not the same. While it is possible to sell off-the-shelve ERP software, the software still needs options for customization through configuration and parameterization. 

These configuration options result in additional complexity within the code. Every parameter adds branches through the control flow and requires additional tests and effort during code changes. The developer needs to understand all these different paths, and more important, be able to predict the influence of his change on all these paths.

The third challenge that we faced was **the mix of domain knowledge and technical knowledge in one code base**. While functionality has a certain evolution path (law, improvements, new branches), technology has a completely different pace (move from on-premise to cloud for instance). Not only the pace is different, it is also difficult to have expert level domain knowledge and have the technical skills to build and maintain a large system. While teams work closely together, we still end up with creating functional requirements and designs that a technical specialist translates into code.

We knew that if we would do a straight-forward rewrite of the ERP system, we would end up with the same mix a couple years down the line. What we needed was a clear separation of the two concerns that would allow us to evolve them in a different pace. And maybe even involve the business analysists more with the functionality expressed in code.

## Making the domain a first-class citizen

We found a solution for our challenges in the utilization of model-driven development (MDD). Model-driven development is claimed to increase both productivity and quality, while lowering complexity by raising the level of abstraction. By creating a meta-model[^meta] of the domain, instances of that meta-model can be created to describe the software on a higher level. An automated process, or generator, then translates this model into running software.

[^meta]: A meta-model in MDD is like a domain specific language, but does not need a concrete syntax.

The domain of the software itself is expressed in the meta-model and is thus pulled out of the actual source code. This allows us to bring our code re-use to a new level, because many instances of a single pattern can be translated into running software by a single transformation. It also enables a new level of variability: by changing the model the system changes. Variability is at the core of the system. Finally, it enables us to separate functionality and technology, and let them evolve at different rates.

The development process that we started based on this approach consists of four simple steps:
1. Extract patterns from the existing business logic and formalize those patterns in a meta-model.
2. Use that meta-model to create a model of the business logic in an ERP system.
3. Generate a working application from that model.
4. Evaluate the working application, and when necessary start at 1.

These steps might appear simple, however, executing them is not that easy. And while MDD is a large research field with promising results, it also has its share of failed projects. However, we believe there are two important reasons why we can pull this off. 

First, we are in the ERP business for almost 20 years. We know our domain. We have built it, and we are shipping ERP software as we speak. We have a large group of experts in our company, and we have an even larger group of customers that show us how they use our software and what they need. 

Second, we are not trying to build an MDD platform that allows you to build a large variety of software systems. The platform is only used to build our own ERP system, the platform itself is not the product, it is a tool for us to develop our product. We know the boundaries and scope of our domain. We do not have to solve every problem. We only need to solve our own, ERP related, problems.

## One bounded context

As mentioned, we discovered DDD through CQRS and event-sourcing. And we choose to generate a CQRS, event-sourced system from the model, because we believed in the scale and flexibility it would provide us. However, in the initial versions of our platform we still had two monoliths: our generator, and the generated CQRS application. One of the biggest inspirations that we have found in DDD was the concept of bounded contexts, of different sub-domains, and the idea that the DRY (don’t repeat yourself) rule should only be used within a bounded context[^boundaries].

[^boundaries]: <https://medium.com/russmiles/on-boundaries-and-microservices-d559ec52bb55>

The resulting application was a monolithic deployment unit. With every change of the model, we needed to generate the complete application, and deploy it. Now, it isn’t impossible to do (we are doing it, and even manage to deploy a new application with zero-downtime through blue-green deployments), but the deployment feels bigger and more cumbersome than necessary. We feel that this kind of upgrades will not scale and that it will become a problem later one, when the model starts evolving at an increased speed. 

We also had a single monolithic generator that translated the complete model. This became a burden when both the meta-model (the number of possible patterns increased) and the development team grew. The monolithic generator had several generic possibilities, and new features needed to be solved in the same generic way. This let to sub-optimal solutions. It also made the generator very complex. There were so many possible execution paths that no-one was able to reason about them. We all lost the big picture of the generator. We tried to solve these problems by 
1. introducing abstraction (*as we all know; every problem can be solved by adding more indirection[^indirection]*). 
2. refactoring our generator into a multi-stage generator. The parsed model was transformed, extended, simplified, translated into intermediate models, before generating the final output. 

[^indirection]: "Any problem in computer science can be solved with another level of indirection." is attributed to David Wheeler by **Diomidis Spinellis**. [Another level of indirection](https://www2.dmst.aueb.gr/dds/pubs/inbook/beautiful_code/html/Spi07g.html). In Andy Oram and Greg Wilson, editors, Beautiful Code: Leading Programmers Explain How They Think, chapter 17, pages 279–291. O'Reilly and Associates, Sebastopol, CA, 2007.

In the long run this did not work out. We still had a single transformation pipeline on which the whole team was working. The development work was not scaling, because we were getting in the way of each other. There was no real code ownership, so no team felt responsible. And finally, it made it hard to implement an incremental generation flow. 

With the huge amount of code that we were generating, we knew we had a new challenge to face. Two major steps took us from these two single bounded contexts (the generator and the resulting application) into a new realm of multiple bounded contexts:
1. The move from a single code generator into a collection of small generator *modules*.
2. The move from a monolithic runtime application into a platform and many loosely coupled *bundles*. 

## A swarm of generators

Generating an application involves a lot of steps. The input model is analysed, and patterns are translated into concepts that fit the target platform. While we were extending the meta-model and handling new target components, our generator became a big ball of mud.

As already mentioned, we tried to mitigate this by adding abstractions and by added different phases in the generator. But we were not able to untangle our big ball of mud. The solution was found in the concept of different bounded contexts.

We started to hard work of breaking up our monolithic generator into several smaller generators: *modules*. A module is in fact a mini-generator, responsible for specific model elements in the meta-model. One module might transform the elements of type x, while another transforms the elements of type y. How many instances of a pattern are present in a model is not important, the module will translate all occurrences into code that matches the target platform.

We made the different patterns in the meta-model the bounded contexts of our generator. A module is an independent component in the generator. It receives the model as input and delivers output. How a module works is a matter of implementation detail. It could be through model transformations and intermediate models, but it could also be in a single step. A module truly forms a bounded context in the generator: it uses its own language and makes its own decisions. 

Every team is responsible for a number of these modules. There is clear ownership and responsibility, but there is also freedom. This allows our teams to move fast, without being hindered by the complexity of other parts of the generator.

Of course, this does introduce code duplication: several modules might need to make the same analysis or transformation. If these modules are developed by the same team, they can easily choose for reuse. However, it becomes more complex when these modules are developed by different teams. These scenarios are dealt with on a case-per-case basis. Some are solved with shared libraries, while some are not solved at all. 

## Breaking up the monolith in bundles

As explained, our runtime application architecture is based on CQRS and event-sourcing. We generated components such as aggregates, commands, events, and projectors from the input model. Still, our application was a distributed monolith in terms of deployment and upgradability.

When we started out, we generated C# and packaged everything in DLL's. And because our generator was monolithic, these DLL's contained all kinds of different functionality. A change to some small part meant that we needed to upgrade several DLL's at once.

Our second move started with the recognition of bounded contexts in our resulting application. Of course, there are many different parts in an ERP system, and our goal was the ability to update them individually. We needed to separate them, and we did that by no longer generating C#.

The process flow in any MDD platform is quite simple, when zoomed out: parse the model, analyse it and transform it into an executable form. That is the 'code generation' flow. When using interpretation, the process flow is a bit different. The executable is already there, and it parses the model, analyses it, and executes it. The main difference between code generation and interpretation is thus the moment in time when the model is parsed, analysed and executed. With code generation, the model is parsed and analysed well before any end-user touches the system. With interpretation, the model is parsed and analysed around the same time that the end-user touches the system.

We decided to move towards a hybrid form: we generate an intermediate language (in our case consisting of JSON files) that is interpreted at run-time. This intermediate language enables us to deploy smaller parts of the application, parts that we call *bundles*. The idea behind a bundle is that it is some isolated piece of functionality that should be deployable and upgradeable on its own. Technically, they’re just some JSON files. You could see them as microservices, but we prefer to call them bundles.

A nice benefit of the move towards these definition files that are interpreted is that it allows us to upgrade the application without restarting the process. A .NET process cannot reload DLL's while running. It needs to be stopped, the DLL's need to be replaced, and then the process can be started. We can, however, update the JSON files, and the application can pick up the changes without being restarted. This gives us much more flexibility when it comes to upgrading.

It also allows us to create a multi-tenant host process that contains applications for different customers. The process can be shared between applications, giving us an improved resource usage. The underlying framework, with interpreters and other components, is what we are calling the 'platform'. It is our custom developed runtime platform that hosts the bundles and makes sure that everything works.

## Final words

The move to modules and bundles has made us more agile and more flexible. Because of the recognition and application of bounded contexts in both the generated application and the generator we are in control again. 
Are there only upsides? No, as with every design decision there are trade-offs.

*	We lose opportunities for reuse. While we explained that this is deliberate (only do DRY in a bounded context), it is still a discussion that we have every now and then. We try to mitigate this with small libraries, or by refactoring our bounded contexts. And in the long run: it is a deliberate choice we made.
*	Debugging and analysing the JSON files at run-time is a lot harder than reading C# code. 
*	Upgrading the monolithic application with a blue-green strategy is far easier than upgrading several loosely coupled microservices that have some relation to each other. Our upgrade scenarios have become more complex.
*	Finding the right bounded contexts is in fact hard work. Throwing everything together is easier than really thinking about boundaries and dependencies.
*	We have lost safety in the generation process. The compilation of C# gave us a warning when different parts were not aligned. With the generation of JSON files we lose that warning. 

Now of course, we do try to mitigate some of these challenges. We have, for instance, added explicit usage of contracts between bundles. Every bundle can provide and assume API's. The 'assumptions' are linked to the 'provides', and by doing that we get a graph of the bundles. The resulting graph forms the base for our consistency check and give us insight in the message flows in our application. 

We are not yet at the end of our journey. There is road that needs to be walked, until we go live. And while walking that road we will let the great ideas in the DDD community inspire us!
