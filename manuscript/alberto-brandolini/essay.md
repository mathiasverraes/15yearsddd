# Discovering Bounded Contexts with EventStorming (by Alberto Brandolini)

There's plenty of outcomes from a Big Picture EventStorming, the most obvious being the collective learning that happens throughout the workshop. But learning is definitely not the only one!

In this essay we'll see how EventStorming can be leveraged in order to discover candidate bounded contexts in a complex domain.

## Why Bounded Contexts are so critical

Among the many ideas coming with Domain-Driven Design, Bounded Contexts have been initially hard to grasp, at least for me. It took me a while to realize how powerful and fundamental this concept is.

In 2004, I was probably too good in building monoliths, or maybe I just hadn't seen anything different yet. In a few years, after seeing a few consequences of mainstream architectural practices, I radically changed my mind.

Now I consider _“getting the boundaries right”_ the single design decision with the biggest impact over the entire life of a software project. Sharing a concept that shouldn't be shared or that will create unnecessary overlappings between different domains will have consequences spanning throughout the whole sociotechnical stack.

Here is how it might happen.

* A common concept (like the `Order` in an e-commerce web shop) becomes vital for several business capabilities, raising the need for reliability and availability, up to the unexplored limits of the CAP theorem, where buying more expensive hardware can't help you any more.
* Security and access control gets more complicated: different roles are accessing the same information, but _not exactly the same_, hence the need for sophisticated filtering.
* Shared resources require more coordination to be changed: _“we have to be sure”_ we are not breaking anyone else's software and plans. The result is usually more and more meetings, more trade-offs, more elapsed time to complete, and less time for proper software development.
* Since everybody now depends on 'the Order', be it a database table, a microservice or an Order Management System, changing it becomes riskier. Risk aversion will slowly start polluting your culture, necessary changes will be postponed.
* Developers will start calling the backbone software _“legacy”_ with a shade od resentment. It's not their baby anymore, it's just _the thing that wakes them up in the middle of the night_.
* Adding refactoring stories to your backlog becomes a farce: since there is no immediate business value to be delivered, refactoring is being postponed, or interrupted. Your attempts to explain “technical debt” to your non-technical colleagues always leave you disappointed.
* The time it takes to implement changes to the core of your system is now umbearable. Business departments stop asking changes in those areas and are implementing workarounds by themselves.
* Now your workplace isn't just that fun anymore. Some good developers that made it great, are now looking for more challenging adventures.
* The business isn't happy either: delayed software evolution caused some business opportunities to be missed, and new players are moving on the market at a speed that is unconceivable with your current software.

And here you are, yelling at the sky, asking yourself: _“What did we do wrong?”_

And a likely answer is: _“We didn't get the right context boundaries”_

## Finding bounded contexts

Ideally, a bounded context should contain a model tailored around a specific *purpose*. The perfectly shaped tool for one specific job, no trade-offs.

Whenever we realize a different purpose is emerging, we should give a chance to a new model, fitting the new purpose, and then find the best way to allow the two model interact.

![Two distinct purposes should map to two different models, inside different bounded contexts.](images/alberto-brandolini/Two_bounded_contexts.png)

Unfortunately, _a single specific purpose_ is not a very actionable criteria to discover boundaries in our model. The idea of 'purpose' is too vague to draw actionable boundaries: developers might be looking for a clear, well-defined purpose, while business stakeholder might be a little more coarse grained, like “I need an Employee Management Solution[^MINAP]”.

In general, we can't assume the business side to know about bounded contexts. BCs are mostly a software development issue, and the learning loop about them will be closed in software development first.

Put in another way, the business stakeholders are not a reliable source of direct information about bounded contexts. _Asking_ about bounded context will get some information, but the answer, can't be trusted blindly.

It's our job as software architects to discover boundaries in our domain, and this will be more an investigation on a crime scene than a _tick-the-checkboxes_ conversation.

![The knowledge distribution in an organization: a weird combination of knwoledge and ignorance](images/alberto-brandolini/Overlapping_expertises_and_ignorances.png)

Nobody knows the whole truth. Let's stop pretetending somebody can.

## Enter EventStorming

EventStorming is a flexible workshop format that allows a massive collaborative exploration of complex domains. There are now several recipes[^ESR], but the one that better fits our need to discover context boundaries is the **Big Picture EventStorming**: a large scale workshop (usually involving 15-20 people, sometimes more) where software and business practitioners are building together a behavioral model of a whole business line.

At the very root the recipe is really simple:

* make sure all the key people (business _and_ technical stakeholders) are in the same room;
* provide them with an unlimited modelling surface (usually a paper roll on a long straight wall plus some hundreds of coloured sticky notes);
* have them model the entire business flow with **Domain Events** along a timeline.

Ib an EventStorming workshop, domain events — or just _events_ — are not software constructs: they're short sentences written on a sticky note, using a verb at the past tense.

![The simplest possible explanation of a domain event](images/alberto-brandolini/Domain_event_explanation.png)

With a little facilitation magic, in a few hours we end up with a big behavioural model of the entire organization: something like the one in the picture below.

![The output of a Big Picture EventStorming, on a conference organization scenario](images/alberto-brandolini/Big_Picture_conference_scenario.jpg)

A massive flood of coloured sticky notes, apparently. But, as the adagio says, _it's the journey, not the destination_: the process of visualizing the whole business flow, with the active participation of all the key stakeholders, is our way to trigger critical insights and discoveries.

## Structure of a Big Picture workshop

To make things clearer, let's see the main steps in the workshop structure, focusing mainly on the steps that provide key insights to Bounded Contexts discovery.
[FIXME: decide what to do with the steps which are not relevant]

### Step 1. Chaotic Exploration

This is where workshop participants explore the domain, writing verbs at past tense on sticky notes (usually orange), and place them on the wall, according to an ideal timeline.

The key trick here is that nobody knows the whole story. Imagine we're exploring the domain of conference organization[^CALM]: there will be roles that know about strategy and market positioning, others specialized in dealing with primadonna speakers, plus a variety of other specialists or partners dealing with video coverage, catering, promotional materials and so on.

If you know one job really well, you probably won't have time to know every other job at the same depth. And ...that's exactly what we're expecting to find in every business: local experts, masters of their own silo, with variable degrees of understanding of the other portions of the business.

The more participants, the harder it will be to actually follow a timeline: diverging perspectives and specialized view on what the business is actually doing will usually lead to **clusters of locally ordered events, in a globally inconsistent whole**.

Far from perfect, but a good starting point. Now we see stuff.

![The possible outcome of a chaotic exploration round in a Big Picture EventStorming.](images/alberto-brandolini/ES_Big_picture-after_chaotic_plus_notes.png)

Moreover, this first step is usually _quiet_: people will silently place their own personal braindump on the wall, wherever there's enough space available. Not so many conversations happening. Next steps will be noisier.

#### Divergence as a clue

Actually, we want this phase to be quiet: people should not agree yet about what to write on sticky notes. The facilitator should make sure that there is plenty of markers and stickies so that everybody can write their own interpretation of the flow independently, without influencing each other too much.

As a result, we'll end up with a lot of _duplicated_ sticky notes, or _apparently duplicated_ ones.

![Different wordings are often a clue of different underlying meanings.](images/alberto-brandolini/ES_Big_picture-duplicated_events.png)

It's usually a good idea to resist the temptation to resolve those duplicates and find and _agree_ on a single wording choice. Different wording may refer to different perspectives on the same event, hinting that this might be relevant in more than one Bounded Context, or that the two or more events aren't exactly the same thing.

Getting back to our conference scenario, we might expect to have a few domain events referring more or less to the same thing, with different wording. Something like `Schedule Ready`, `Schedule Completed`, `Schedule Published` and so on.

This is already telling us something: this event (assuming or pretending there's only one event here) is probably relevant for different actors in the business flow.

That's cool! This might be a hint of multiple overlapping contexts.

![Different meanings may point to different models, hence different contexts.](images/alberto-brandolini/ES_Big_picture-duplicated_events_maybe_overlapping_contexts.png)

I didn't say _“bounded”_ because the boundaries aren't clear yet.

### Step 2. Enforce the Timeline

This is where we ask participants to make sure there is a solid timeline describing the business flow from a beginning to an end.

It won't be that easy: there'll be parallel and alternative paths to explore. Even big-bang business like conference organization tend to settle on a repeating loop, usually repeating every year.

But what really happens here is that the need to come up with _one consistent view_ of the entire business triggers some **conversations** around the places where this view is not consistent. People start asking questions about what happens in obscure places, and they get answered, because we made sure the _experts are available!_

At the same time, we'll have diverging views about how a given step should be performed. Some conflicts will be settled — after all it's just a matter of having a conversation — other will be simply highlighted with a **Hot Spot** (usually a sticky note in the red spectrum, like magenta), to let the exploration flow.

[FIXME: picture of a hotspot.]

HotSpots clarify the underlying approach of our exploration: we're not here to _solve everything_, there is simply no time for that. But we can try to _visualize everything_ including things that are unclear, uncertain or disputed.

The Big Picture EventStorming will deliver **the snapshot of our collective current level of understanding of the business** including holes and gaps.

### Emerging structure

Simply talking about problems and moving sticks around won't do justice to the insights and discoveries happening during this phase. This is where participants often look for a more sophisticated structure, to sort out the mess they just created.

There are a few strategies to make the emerging strucure visible. The most interesting for discovering bounded contexts are *Pivotal Events* and *Swimlanes*.

#### Using Pivotal Events

Pivotal Events are specific events which are particularly relevant for the business, and usually set a transition between different business phases.

In our conference organization we might spot a few candidates.

* `Conference Website Launched` or maybe `Conference Announced`: this is when you may start to sell tickets, but at the same time you can't easily withdraw anymore.
* `Conference Schedule Announced`: now, the speakers are officially in. And ticket sales should start.
* `Ticket Sold`: on one side, here is a relevant business transaction, with money finally coming in; on the other one, we now have a *customer* and/or an *attendee* and a lot of specific communications that we'll have to manage.
* `Conference Started`: this is where attendees are expecting to get some value back from the ticket they purchased. Same goes for speakers looking for insights or contacts, and sponsors.
* `Conference Ended` looks like an obvious one. The party is over, let's deal with the aftermaths.

I usually mark the candidate events with a colored tape, so that they're visible and we have a visible hint of distinct phases.

![A coloured replaceable tape is my favorite tool for marking pivotal events](images/alberto-brandolini/ES_Big_picture-Pivotal_Event.png)

It actually doesn't matter to pick the right ones, so I often keep this discussion short. I look for 4-5 candidate events that seems to fit that role. Mostly in order to sort out the internal events faster.

After highlighting pivotal events, sorting becomes a lot faster inside the boundaries, and a more sophisticated structure starts to emerge.

![Pivotal Events are a great source of information](images/alberto-brandolini/ES_Big_picture-pivotal_events.png)

#### Using Swimlanes

Even in the most trivial businesses, the flow is not linear. There are branches, loops and things that happen in parallel. Sometimes the touch points between different portions of the flow are well-defined, like _billing_ getting triggered only around the events of a sale, or maybe a cancellation. Other times, the relationship can be more complicated: announcing some famous speaker can boost sales, sales can attract sponsors, sponsorships can allow organizers to afford the paycheck for more superstars speakers, which can trigger more sales and eventually trigger a venue upgrade.

**Horizontal Swimlanes** is a common way to structure portions of the whole flow. It usually happens after pivotal events, but there's no strict recipe here: the emerging shape of the business suggests the more effective partitioning strategy.

In our conference scenario, we can spot a few main themes that happen more or less in parallel: a _Speaker Management Flow_ dealing with theme selection, call for papers and invitation, logistics and accommodation; a _Sales Management Flow_ dealing with ticket sales, advertising, logistics and everything needed to welcome attendees, a _Sponsor Management Flow_ managing the other revenue stream; and last but not least a lot of not so ancillary areas, from venue management, to catering, staffing, video recording and so on.

Our replaceable tape comes in handy also to gine a name to these parallel flows. The underlying structure backbone, now will look something like this:

![Pivotal Events and Swimlanes provide an emergent structure on top of the flow of Domain Events.](images/alberto-brandolini/ES_Big_picture-multiple_sorting_strategies.png)

Everybody now sees the different _phases_ of the business and the key relevant issues at every step.

### Step 3. People and Systems

This is when we start exploring the surroundings of our business, explicitly lookingh for **people**: actors, users, personas, or specific roles in our system; and **systems**: from software components and tools to external organizations. Nothing excluded.

![Here's the incredibly simple notation for people and systems](images/alberto-brandolini/People_and_systems.png)

Visualizing different actors in our system — we actually don't call them _actors_ just _people_ — helps to dig into the different perspectives. We might discover explict responsabilities and roles, or conflicting perceptions: all speakers are submitting talks, but the treatment can be different if we're talking about a superstar guest which is invited as a keynote speaker, an expert or a newbie. A puzzled look during this exploration phase may end up in opening a completely new branch, or making different strategies more visible and readable.

Systems usually trigger a different reasoning. On one hand, they make our boundaries explicit. We won't be able to deliver value in a vacuum, with self-contanied software: there will be tools, integrations, and so on, in order to complete the flow. Payment management systems, ticketing platforms, social media platforms, video streaming, billing software, and whatever comes to mind.

But systems can also be external entities like government agencies, or simply “the weather” (which might be a tough constraint if you are organizing a conference in extreme regions, or if you're so lucky to get a snow storm the day before).

From the software perspective, an external system calls for some type of integration (maybe our all-time favourte: the Anti-Corruption Layer), but from the business perspective, external systems often impose constraints, limitations or _alibis_, a free scapegoating service if anything goes wrong.

### Step 4. Explicit Walkthrough

Every step triggers some clarification, and prompts writing more events. Even if we added some structure, with pivotal events and swimlanes, and had some interesting conversation on the spot, the whole thing still feels messy. Probably because it is still messy.

It's now time to validate our discoveries, picking a _narrator_ trying to tell the whole story, from left to right. This is really hard, at the beginning because the narrators' brain will be literally be torn apart by conflicting needs: they'll try to tell the story using the existing events as building blocks, but at the same time they'll realize that what seemed _good enough_ in the previous reviews is not good enough for a public _on stage_ storytelling session.

This is when our model needs to be improved in order to support storytelling. Some more events will be written, others will be moved away, paths will be split and so on.

The audience should not be passive. They're challenging the narrator and the official storytelling, eventually providing examples of corner cases and 'not-so-exceptional-exceptions'.

The more we progress along the timeline, the more clarity is provided to the flow, while the narrator is progressing like a _defrag cursor[^IYOETR]_.

![An explict walkthrough round is our way to validate our understanding](images/alberto-brandolini/ES_Big_picture-walkthrough.png)

### Extra steps

There's a few extra steps that might be performed now, usually depending on the context, that may provide more insights. I'll describe them briefly.

* We sometimes explore the **value** that is supposed to be _generated_ or unfortunately _destroyed_ in the business flow. We explore different currencies: money being the most obvious one, often to discover that other are more interesting (like _time_, _reputation_, _emotional safety_, _stress_, _happiness_, and so on).
* We explore **problems** and **opportunities** in the existing flow, allowing everyone to signal issues that didn't suerface during the previous steps, or to make improvement ideas visible.
* We might challenge the status quo with an **alternative flow**: once the understanding of the current situation is settled, what happens if we change it? Which parts are going to stay the same and which one are going to be radically changed or dismissed?
* We might **vote then most important issue** in order to leverage the clarity of collective understanding into political momentun to do the right thing.

All this stuff, plus more, is usually awesome! But most of the information needed to sketch context boundaries is already available, if you take a closer look.

Deriving this information from our workshop is now our job as software architects.

## Homework time

Once the workshop is officially over, and participants left the workshop room, we can start talking software, ..._finally!_

I used to draw a lot of context maps, as a way to _force myself to ask the right questions early in the project_, now I run EventStorming workshops, and I engage stakeholders in providing the righty answers without asking the corresponding questions.

There's a lot of Bounded Context related info that comes as a byproduct of our discussion, we just need to be able to decypher the clues. So, here we are with some heuristics[^IUTWHJTMMH], that may come in handy.

### Look at the business

...or like detectives would say: _“follow the money”_. Businesses are usually built around a well-defined business transaction where some value — usually money — is traded for something else. Pivotal events have akey role in this flow: we won't be able to sell tickets online without a website, everything that happens before the website goes live is _inventory_ or _expenses_, we can start make money only after the `Conference Website Launched` event.

Similarly, after `Ticket Sold` events, we'll be the temporary owners of attendees' money, but they'll start to get some value back only around the `Conference Started` event. But the tools and the mental model needed in order to _design_ a conference, are not the same tools needed to run a conference.

### Look at the people

 people
[FIXME: from here.]

#### Look at the body language

#### Look at the language (or _listen_)


![Emerging bounded contexts after a Big Picture EventStorming](images/alberto-brandolini/Emergent_Bounded_Context.png)


[^MINAP]: Management is not a purpose. This is true on so many levels, but talking about bounded contexts this is especially true: _planning_, _designing_, _tracking_, _running_, _supporting_, _choosing_ are more fine-grained purposes, that often require a model on their own.

[^ESR]: The best entry point to start exploring the EventStorming world is probably the official website at [eventstorming.com](https://www.eventstorming.com).

[^CALM]: Conferences are a little mess, but they are interesting because they often employ fewer people than the required roles: a small team is taking care of various activities spread around months, with a peak of intensity diring the conference and the few days before. The need for specialization is continuously at odd with the need of having to sync as few people as possible. At the same time, I've never seen two conferences alike, so I won't be revealing special trade secrets here.

[^IYOETR]: If you're old enough to remember what _defrag_ used to be. ;-)

[^IUTWHJTMMH]: I mighgt have used the word _'heuristic'_ here just to make Mathias Verraes happy.
