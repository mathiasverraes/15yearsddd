# Discovering Bounded Contexts with EventStorming (by Alberto Brandolini)

In my experience, _bounded contexts_ have always been my favorite DDD thing. They're hard to grasp at first, but getting the boundaries right is probably the single action with the biggest impact on the whole project.

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
