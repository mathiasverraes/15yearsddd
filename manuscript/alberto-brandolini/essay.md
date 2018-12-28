# Discovering Bounded Contexts with EventStorming (by Alberto Brandolini)

Among the many ideas coming with Domain-Driven Design, Bounded Contexts have been initially hard to grasp, at least for me. It took me a while to realize how powerful and fundamental this concept is.

I was probably too good in building monoliths at that time, and I hadn't seen anything different yet. In a few years, after seeing a few consequences of mainstream architectural practices, I radically changed my mind.

Now, "getting the boundaries right" is probably the single design decision with the biggest impact on the entire life of a software project. Sharing a concept that shouldn't be shared or that, will create unnecessary overlappings between different domains with consequences spanning through the whole sociotechnical stack.

* A common concept (like the `Order` in an e-commerce web shop) becomes vital for many different business capabilities, raising the need for reliability and availability, up to the unexplored limits of the CAP theorem.
* Security and access control becomes more complicated: different roles are accessing the same information, but _not exactly the same_, hence the need for sophisticated filtering.
* Shared resources require more coordination to be changed: we have to be sure we are not breaking anyone else's software and plans. The result is usually more and more meetings, more trade-offs, more elapsed time to complete, and less time for proper software development.
* Since everybody is now depending on 'the Order', be it a database table, a MicroService or an Order Management System, changing it becomes riskier. Risk aversion will slowly start polluting your culture, necessary changes will be postponed.
* Developers will start calling the backbone software _"legacy"_ with a shade od resentment. It's not their baby anymore, it's just _the thing that wakes them up in the middle of the night_.
* Adding refactoring stories to your backlog becomes a farce: since there is no immediate business value to be delivered they keep being postponed, or interrupted, while your attempts to explain technical debt to your non-technical colleagues always leave you disappointed. 
* The time it takes to implement changes to the core of your system is now umbearable. Business departments stopped asking changes in those areas and are implementing workarounds by themselves.
* Now your workplace isn't just that fun anymore. Some good developers that made it great, are now packing looking for more challenging adventures. 
* The business isn't happy either: arrested software evolution caused some business opportunities to be missed, and new players are moving on the market at a speed that is unconceivable with your current software.

And here you are, yelling at the sky, asking yourself: _"What did we do wrong?"_




The reason for thai is in their intrinsic _asymmetry_ of behaviour. Think Lego boxes: it takes seconds to open two of them and mix all the pieces on a table. It will take probably half an hour to separate them. Interestingly, mixing _three_ lego boxes won't take much more, but separating them will take a significant amount of extra time.

Bounded contexts behave more or less in the same way: the moment we mix something that shouldn't be mixed (usually sharing a database) we open the door to interdipendencies that shouldn't be there. It's not only _coupling_ at the software level. It's meetings that shouldn't be called for coordinating things that should be independent. Is the continuous lack of safety, or the fear of breaking someone else's code, that ulrimately leads to stagnation, because ...well, you never know.

## Finding bounded contexts

Ideally, a bounded context should contain a model tailored around a specific purpose. The perfect tool, for one specific job. No trade offs. 
The moment we realize we have a different purpose, we should give a chance to a new model, tailored around the new purpose, and then find the best way to allow the two model interact.

However, _single purpose_ is not a very actionable criteria for finding boundaries in our model. The idea of purpose is too ambiguous to draw actionable boundaries: developers might be looking for a clear, well defined purpose, while business stakeholder might be a little more coarse grained.

In general, we can't assume the business side to know about bounded contexts. They are mostly a software development problem, and the learning loop about them will be closed in software development first.

Put in another way, the business stakeholders are not a reliable source of direct information about bounded contexts. _Asking_ about bounded context will get some information, that could not be trusted blindly.

## Enter EventStorming

EventStorming is a flexible workshop format that allows a massive collaborative exploration of a very complex domain. There are now several recipes[^ESR], but the one that better fits our need to discover context boundaries is the **Big Picture EventStorming**: a large scale workshop (usually involving 15-20 people, but I facilitated workhsops with more than 30) where software people and business people are building together a behavioral model of the entire business.

At the very root the recipe is really simple:

* make sure all the key stakeholders are in the same room;
* provide them with an unlimited modelling surface (usually a paper roll on a long straight wall plus some hundreds of coloured sticky notes);
* have them model the entire business flow with **Domain Events** along a timeline.

With a little facilitation magic, in a few hours we end up with a big behavioural model of the entire organization: something like the one in the picture below.

![The output of a Big Picture EventStorming, on a conference organization scenario](images/alberto-brandolini/Big_Picture_conference_scenario.jpg)

There's plenty of outcomes from a Big Picture EventStorming, the most obvious is the collective learning that happens when the different perspective are merged in a flow of events that _has to be consistent_ in order to support storytelling.

### A subsection


![Emerging bounded contexts after a Big Picture EventStorming](images/alberto-brandolini/Emergent_Bounded_Context.png)

### Using Pivotal Events


![Pivotal Events are a great source of information](images/alberto-brandolini/ES_Big_picture-pivotal_events.png)

#### Look at the business

#### Look at the people

#### Look at the body language

#### Look at the language (or _listen_)

### Using Swimlanes


## When to draw our context map




[^ESR]: The best entry point to start exploring the EventStorming world is probably the official website at [eventstorming.com](https://www.eventstorming.com) 
