# Time (by Jérémie Chassaing)

## Buried and scattered

File after file, project after project, finding traces of time in systems seems like a giant treasure hunt. Digging deep in the stack, shoveling heaps of code, turning classes over, time is nowhere to be found.

Hints take the form of asynchronous entry points, timers, threads and locks. Concurrent data access or synchronization primitives. Be it a date or a duration, meaning is shattered and understanding lost.

From a Domain-Driven Design practitioner perspective, it's obvious that there is something missing. A disturbing lack of model.
 
## The essence of Time

Everyone knows what time is, but… giving a definition is not so easy.

A glimpse at [Wikipedia](https://en.wikipedia.org/wiki/Time) surely gives some clues:

> **Time** is the indefinite continued progress of existence and events that occur in apparently irreversible succession from the past through the present to the future. **Time** is a component quantity of various measurements used to sequence events, to compare the duration of events or the intervals between them, and to quantify rates of change of quantities in material reality or in the conscious experience. \[…\]

but the following warning clearly states that there will be no single answer:

> **Time** has long been an important subject of study in religion, philosophy, and science, but defining it in a manner applicable to all fields without circularity has consistently eluded scholars. \[…\]

This definition is referring to duration, that is actually referring to time...Maybe a more formal and physical definition could settle this.

The universal unit of time is the second. Since 1967 it is defined by the [International System of Units](https://www.bipm.org/en/publications/si-brochure/second.html) (SI) in this precise way:

> The second is the duration of 9 192 631 770 periods of the radiation corresponding to the transition between the two hyperfine levels of the ground state of the caesium 133 atom.

The second is defined as a count of transitions. But those transitions are not Time. Transitions are just points in time.

There is something between those points, and this is precisely where time is. Time is the *nothingness* between those events. 

## Events

Let’s step back a bit.
 
How do we feel time passing? By looking at a watch?
 
Then how to explain that an hour sometimes seems so long and sometimes passes in a flash?
 
Time seems slow and empty when we’re bored while Time seems fast and full when we're busy with interesting things. 

Boredom is not caused by the fact that nothing happens. Since there are actually always things happening. Clocks keep ticking, cesium atoms transitioning, the world spinning. But boredom still happens because these events seem of low interest to its subjects.

Events that don't affect the subject are filtered. Only events that change the subject substantially get noticed and are remembered.

The interesting or noteworthy things that happen act on personal state and change it. These are **meaningful events**. Things that happens and change people deeply.

Of course a lot of things happen between those meaningful events like moving and thinking. The blood flows through the body, but this is just a maintenance move. So it goes unnoticed. And maybe some things happen between state transition of a cesium atom, but since it's not possible to notice it and give it a meaning for now, it has no influence and just doesn't actually exist.

This perception of meaningful events is surely a reason why people say the time pass faster when old. In the 6 first years, any event is meaningful for kids. "Look dad! A white car! And here another one, and there another one!" Any event makes them change since they have no previous knowledge. Then has time goes by, people integrate knowledge and filter things they already know, they’ve already seen. When old, a year can more easily seem the same than the year before.

But some people continue to enjoy and learn as much as they can to still have a [long now](http://longnow.org/essays/big-here-long-now/).

But when a meaningful event happens, the subject changes and is not the same before and after.

This is what time is about, and that's the reason it is one way.

**Before >> Event >> After**

*Events define time by causality*

## Time inside Systems

Tracking changes in systems is usually done by adding log and timestamps at strategic points. But it's seldom done initially. It's generally added later in the process to help understant when things go wrong.

Now, looking at the problem with a new understanding of Time it becomes clear that *Systems never change for no reason*. It’s always because a meaningful event happened.

This event can be caused by a user interaction, a call from an external system, a sensor trigger… It can also be following by another event. But there is always a reason. 

And when things change because it’s midnight? It simply means that midnight is a meaningful event in the system. And this meaning has to be found. In financial markets, a lot of things happen a 4PM. But it's not due to the fact that it's 4PM. It's actually because the bell rang, and the market is closing. Noticing that the close bell rang is the reason, it makes it fare easier to handle the case when the bell rings earlier due to market exceptional situations, like market crash.

Where are those meaningful events in the System? Hidden in infrastructure code?
 
Greg Young would say:

> Make the implicit explicit!

## Domain Events
 
There is no change in the domain that is not due to an Event. And Domain-Driven Design should definitely encompass them to create better models when time passing in the system is part of the problem.

Once starting to look for them, events appear everywhere in the Ubiquitous Language:

* When the client **has moved** to a new location, send him a welcome kit.
* When a **room has been overbooked** try to relocate the customer
* Every day at midnight, when **day changed**, evaluate last minute prices.

In all domains that are business related, Domain Events are relevant. They have to deal with time because business is mostly about time and money.

By introducing Domain Events in a domain model, Events and Time become explicit in the domain.

Time is now part of the Ubiquitous language and it becomes easier to provide a clear implementation for it.
