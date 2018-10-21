# Discovering Bounded Contexts with EventStorming (by Alberto Brandolini)

In my experience, _bounded contexts_ have always been my favorite DDD thing. They're hard to grasp at first, but getting the boundaries right is probably the single action with the biggest impact on the whole project.

Ideally, a bounded context should contain a model tailored around a specific purpose. The perfect tool, for one specific job. No trade offs. 
The moment we realize we have a different purpose, we should give a chance to a new model, tailored around the new purpose, and then find the best way to allow the two model interact.

However, _single purpose_ is not a very actionable criteria for finding boundaries in our model. The idea of purpose is too ambiguous to draw actionable boundaries: developers might be looking for a clear, well defined purpose, while business stakeholder might be a little more coarse grained.

In general, we can't assume the business side to know about bounded contexts. They are mostly a software development problem, and the learning loop about them will be closed in software development first.

Put in another way, the business stakeholder are not a reliable source of direct information about bounded contexts. _Asking_ about bounded context will get some information, that could not be trusted blindly.

## Enter EventStorming

EventStorming is a flexible workshop format that allows a massive collaborative exploration of a very complex domain. There are now several recipes[^ESR], but the one that better fits



At the very root the recipe is really simple:

* make sure all the key stakeholders are in the same room;
* provide them with an unlimited modelling surface (usually a paper roll on a long straight wall plus some hundreds of coloured sticky notes);
* have them model the entire business flow with **Domain Events** along a timeline.

![The output of a Big Picture EventStorming](images/alberto-brandolini/Big_Picture_conference_scenario.jpg)

### A subsection


[^ESR]: The best entry point to start exploring the EventStorming world is probably the official website at [http://www.eventstorming.com](!http://www.eventstorming.com) 
