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

And the answer is: _"We didn't get the right context boundaries"_

## Finding bounded contexts

Ideally, a bounded context should contain a model tailored around a specific *purpose*. The perfectly shaped tool for one specific job, no trade offs.

The moment we realize a different purpose is emerging, we should give a chance to a new model, fitting the new purpose, and then find the best way to allow the two model interact.

![Two distinct purposes should map to two different models, inside different bounded contexts.](images/alberto-brandolini/Two_bounded_contexts.png)

Unfortunately, _a single specific purpose_ is not a very actionable criteria for finding boundaries in our model. The idea of purpose is too ambiguous to draw actionable boundaries: developers might be looking for a clear, well defined purpose, while business stakeholder might be a little more coarse grained, like "I need an Employee Management Solution".

In general, we can't assume the business side to know about bounded contexts. BCs are mostly a software development issue, and the learning loop about them will be closed in software development first.

Put in another way, the business stakeholders are not a reliable source of direct information about bounded contexts. _Asking_ about bounded context will get some information, that could not be trusted blindly.

It's our job as software architects to discover boundaries in our domain, and this will be more an investigation on a crime scene than a _tick-the-checkboxes_ conversation.

## Enter EventStorming

EventStorming is a flexible workshop format that allows a massive collaborative exploration of complex domains. There are now several recipes[^ESR], but the one that better fits our need to discover context boundaries is the **Big Picture EventStorming**: a large scale workshop (usually involving 15-20 people, but I facilitated workhsops with more than 30) where software people and business people are building together a behavioral model of the entire business.

At the very root the recipe is really simple:

* make sure all the key stakeholders (business _and_ technical) are in the same room;
* provide them with an unlimited modelling surface (usually a paper roll on a long straight wall plus some hundreds of coloured sticky notes);
* have them model the entire business flow with **Domain Events** along a timeline.

With a little facilitation magic, in a few hours we end up with a big behavioural model of the entire organization: something like the one in the picture below.

![The output of a Big Picture EventStorming, on a conference organization scenario](images/alberto-brandolini/Big_Picture_conference_scenario.jpg)

There's plenty of outcomes from a Big Picture EventStorming, the most obvious is the collective learning that happens when the different perspective are merged in a flow of events that _has to be consistent_ in order to support storytelling.

## Big Picture EventStorming structure

To make things clearer, let's see the main steps in the workshop structure, focusing mainly on the steps that provide key insights to Bounded Contexts discovery.
[FIXME: decide what to do with the steps which are not relevant]

### Step 1 - Chaotic Exploration

This is where workshop participants explore the domain, writing verbs at past tense on sticky notes (usually orange), and place them on the wall, attempting to follow a timeline.

The key trick here is that nobody knows the whole story. Imagine we're exploring the domain of conference organization[^CALM]: there will be roles that know about strategy and market positioning, others specialized in dealing with primadonna speakers, plus a variety of other specialists or partners dealing with video coverage, catering, promotional materials and so on.

If you know one job really well, you probably won't have time to know every other job at the same depth. And ...that's exactly what we're expecting to find in every business: local experts with variable degrees of understanding of the other portions of the business.

The more participants, the harder it will be to actually follow a timeline: diverging perspectives and specialized view on what the business is actually doing will usually lead to **clusters of locally ordered events, in an globally inconsistent whole**.

![The possible outcome of a chaotic exploration round in a Big Picture EventStorming.](images/alberto-brandolini/ES_Big_picture-after_chaotic_plus_notes.png)

Moreover, this first step is usually _quiet_: people will silently place their own personal braindump on the wall, wherever there's enough space available. Not so much conversations happening.

#### Divergence as a clue

Actually, we want this phase to be quiet: people should not agree yet about what to write on sticky notes. The facilitator should make sure that there is plenty of markers and stickies so that everybody can write their own interpretation of the flow independently, without influencing each other too much.

As a result, we'll end up with a lot of _duplicated_ sticky notes, or _apparently duplicated_ ones.

![Different wordings are often a clue of different underlying meanings.](images/alberto-brandolini/ES_Big_picture-duplicated_events.png)

It's usually a good idea to resist the temptation to resolve those duplicates and find and _agree_ on a single wording choice. Different wording may refer to different perspectives on the same event, hinting that this might be relevant in more than one Bounded Context, or that the two or more events aren't exactly the same thing.

Getting back to our conference scenario, we might expect to have a few domain events referring more or less to the same thing, with different wording. Something like `Schedule Ready`, `Schedule Completed`, `Schedule Published` and so on.

This is already telling us something: this event (assuming or pretending there's only one event here) is probably relevant for different actors in the business flow.

That's cool! This might be a hint of multiple overlapping contexts.

![Different meanings may point to different models, hence different contexts.](images/alberto-brandolini/ES_Big_picture-duplicated_events_maybe_overlapping_contexts.png)

I didn't say _"bounded"_ because the boundaries aren't clear yet.

### Step 2. Enforce the Timeline

This is where we ask participants to make sure there is a solid timeline describing the business flow from a beginning to an end.

It won't be that easy: there'll be parallel and alternative paths, to explore and even big-bang business like organizing conferences tend to settle on a repeating loop, usually repeating every year.

But what really happens here is that the need to come up with _one consistent view_ of the entire business, triggers some conversations around the places where this view is not consistent. People start asking questions about what happens in obscure places, and _experts are available!_

At the same time, we'll have diverging views about how a given step should be performed. Some conflicts will be settled - after all it's just a matter of having a conversation - other will be simply highlighted with a **Hot Spot** (usually a sticky note in the red spectrum, like magenta), to let the exploration flow.

[FIXME: picture of a hotspot.]

Using HotSpots clarifies the underlying approach of our exploration: we're not here to _solve everything_, there is simply no time for that. But we can _visualize everything_ including things that are unclear, uncertain or disputed. 

The Big Picture EventStorming will be **the snapshot of our collective current level of understanding of the business** including holes and gaps.

#### Emerging structure

Simply talking about problems and moving sticks around won't make justice to the insights and discoveries happening during this phase. This is where participants often look for a more sophisticated structure, to sort out the mess they just created.

There are a few strategies to make the emerging strucure visible. The most interesting for discovering bounded contexts are *Pivotal Events* and *Swimlanes*.

##### Using Pivotal Events

Pivotal Events are specific events which are particularly relevant for the business, and usually set a transition between different business phases.

In our conference organization we might spot a few candidates.

* `Conference Website Launched` or maybe `Conference Announced` - this is when you may start to sell tickets, but at the same time you can't roll back anymore.
* `Conference Schedule Announced` - now, the speakers are officially in. And tickets should follow.
* `Ticket Sold` - from one side, here is a relevant business transaction; from another one now we have a *customer* and/or an *attendee* and a lot of specific communications will follow.
* `Conference Started` - this is where attendees should get some value back, from the ticket they purchased. Same goes for speakers looking for insights or contacts, and sponsors.
* `Conference Ended` looks like an obvious one. The party is over, let's deal with the aftermaths.

I usually mark the candidate events with a colored tape, so that they're visible and we have a visible hint of distinct phases.

![A coloured replaceable tape is my favorite tool for marking pivotal events](ES_Big_picture-Pivotal_Event.png)

It actually doesn't matter to pick the right ones, so I often keep this discussion short. I look for 4-5  candidate events that seems to fit that role. Mostly in order to sort out the internal events faster.

![Pivotal Events are a great source of information](images/alberto-brandolini/ES_Big_picture-pivotal_events.png)

However there are a few heuristics that might come in handy, if you're stuck.

1. **Look at the business**, or like detectives would say: _"follow the money"_. Businesses are usually built around a well defined business transaction where some value - usually money - is traded for something else. Pivotal events have akey role in this flow: we won't be able to sell tickets online without a website, everything that happens before the website goes live is _inventory_ or _expenses_, we can start make money only after the `Conference Website Launched` event. Similarly, after `Ticket Sold` events, we'll be the temporary owners of a attendees money, but they'll start to get some value back only around the `Conference Started` event.
2. **Look at the people** people
[FIXME: from here.]

#### Look at the body language

#### Look at the language (or _listen_)

### Using Swimlanes



![Emerging bounded contexts after a Big Picture EventStorming](images/alberto-brandolini/Emergent_Bounded_Context.png)

## When to draw our context map




[^ESR]: The best entry point to start exploring the EventStorming world is probably the official website at [eventstorming.com](https://www.eventstorming.com) 

[^CALM]: Conferences are a little mess, but they are interesting because they often employ less people than the required roles: a small team is taking care of many different activities spread around months, with a peak of intensity diring the conference and the few days before. The need for specialization is continuously at odd with the need of having to sync as few people as possible. At the same time, I've never seen two conferences alike, so I won't be revealing special trade secrets here. 
