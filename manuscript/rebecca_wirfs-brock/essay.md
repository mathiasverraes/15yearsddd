# Traces, tracks, trails, and paths: An Exploration of How We Approach Software Design

## Introduction
If I were to be brutally honest about the nature of software design, I would give up on any notion of certainty. The more I know about software and the world it is part of, the more cautious I become about making absolute statements about either. Software design is full of unexpected complexities and continual surprises. I cannot predict which contextual details will suddenly become important. Small details can loom large and undo even the best design intentions.


Because I acknowledge this uncertainty, I seek out other designers’ stories. I want to learn about the ugly, confusing aspects of design that are rarely written about. I want to incorporate others’ insights into my growing understanding of the nature of software design. I want to learn what heuristics they use to solve their design problems and see where they clash with or complement my own.


As a designer I often encounter conflicting goals, dynamically changing context, and shifting degrees of certainty about those heuristics I know and cherish. Once in a while this makes me pause to reflect and readjust my thinking. But more often, I quickly take stock of the situation and move on, perhaps only tweaking my design a little, without much exploration or thought. I don’t spend much time consciously rethinking and rearranging my worldview.


I’m hoping to change that just a little by giving myself some space and time to reflect on how I approach design and share some ways collectively we as designers might grow, alter, articulate, and better share our heuristics. There is much to learn about design from the stories we tell and from the questions we ask of each other.  

## Background
A software designer’s personal toolkit likely includes an awareness of some hardcore technical design patterns (and how to shape and adapt and refine them). It also includes heuristics for how to approach the current task at hand. Our heuristics have been imparted to us through code and conversations, as much as anything. While we may read others’ design advice—be it from patterns or stack overflow replies, the heuristics we’ve personally discovered on our own design journey may be even more important.


In *Discussion of the Method*, Billy Vaughn Koen defines a heuristic as, “anything that provides a plausible aid or direction in the solution of a problem but is in the final analysis unjustified, incapable of justification, and potentially fallible.” If you desire to create or change a system (whether social, political, physical, software, or otherwise), opting for what you consider to be the best available heuristics to apply as you balance conflicting or poorly understood criteria for success, then you are solving an engineering problem. Rarely are such problems well defined. Instead, we problem solvers determine what the actual problem is based on diffuse, changing requirements. And to solve that problem, we successively apply heuristics based on our imperfect knowledge of both the current situation as well as the outcome of taking any specific action. Heuristics offer plausible approaches, not infallible ones.


When we software designers choose an approach to solve a current problem, most of the time we are satisficing—finding a satisfactory approach, not actively judging what’s best or optimal. If a heuristic seems to fit the situation, I try it. Given what I know, what I believe to be salient at the moment, what I intuit, what I value, and what constraints I have, I choose what I think are reasonable heuristics (at whatever granularity they are). There is no guarantee that doing so actually moves me closer to my design goal. Consequently I need to check my emerging solution for flaws or weaknesses. If I spot any, I take corrective action. Sometimes I backtrack a long way, unwinding what I’ve already done in order to try out an alternative design approach. More often than not, I only slightly backtrack, having already committed myself to a path that I want to follow. In that case I’m not willing to invest in finding a totally new approach. And sometimes, even though things don’t seem to be working out, I plow ahead, although I feel uneasy, hoping I’ll be on firmer footing soon. I never proceed in a straight line from problem understanding to solution design in a series of even steps. Instead, I move haltingly forward to a more nuanced understanding of what aspects of my emerging solution are important.


Most of the time, I work on autopilot. I make many decisions and take many design actions, using heuristics at whatever level I need. These heuristics have been deeply embedded into my design gestalt. I apply them without any conscious thought. Only when I bump up against a design challenge where I don’t know what to do next—when there is some tension or nagging uncertainty or unfamiliar territory—do I actively take a step back from what I’m doing to look outside of myself for others’ wisdom. It is when I pop out of this “unconscious action” mode to actively search for a design heuristic that I want to be able to quickly assess the utility of any I might find.


I assert that a well-written pattern is a particularly nicely packaged form of heuristic. Patterns are particularly useful as they are drawn from direct experience and include handy information for the discerning designer—most notably the context where the pattern is useful as well as tradeoffs and consequences of applying it.


Although I like patterns, the vast majority of software design heuristics have not been written in pattern form. Nor do I expect them to be. Not every useful heuristic is a pattern. I seek out those other heuristics, too. I am on the lookout for useful heuristics wherever I am engaged in designing or learning about software design (for example, when thinking about how to solve a current problem that is unfamiliar, when reading code, reading blogs, when playing with a new framework, when searching for online advice and recommendations, when attending conference talks, talking with friends, going to meetups, …). I keep adding to my bag of tricks. I tweak and refine heuristics through experience. Rearranging and growing my heuristics toolkit is ongoing and not in anyway systematic.

## Metaphors for understanding the certainty and utility of different software heuristics we might pick up and use
Could I be a better software designer if I made finer distinctions between heuristics? There are those I know deeply and have learned from others. There are those I discovered on my own. There are heuristics I know intimately—however I came to know them—that I have lovingly polished through experience. And there are those shiny new heuristics I hear or read about.


So what are some ways to understand the soundness and utility of heuristics we find? Robert Moor, in his book, *On Trails*, suggests that we untangle the various meanings and distinctions between trails, traces, tracks, ways, roads, and paths in order to understand how trails came to be and continue to evolve.

>“The words we English speakers use to describe lines of movement—trails, traces, tracks, ways, roads, paths—have grown entangled over the years…But to better understand how trails function it helps to momentarily tease them apart. The connotations of trail and path, for example, differ slightly…the key difference between a trail and a path is directional: paths extend forward, whereas trails extend backward. (The importance of this distinction becomes paramount when you consider the prospect of lying down in the path of a charging elephant versus lying down in its trail). Paths are perceived as being more civilized in part because of their resemblance to other urban architectural projects: They are lines projected forward in space by the intellect and constructed with those noble appendages, the hands. By contrast, trails tend to form in reverse, messily, from the passage of dirty feet.”                                                    —Robert Moor, *On Trails: An Exploration*

Are published software design patterns more like paths or trails? How certain and civilized and planned are these patterns?


I see a resemblance between paths and published pattern collections. Published patterns collections are neatly laid out, organized, and explained. They typically include some sort of map, suggesting connections and arcs of expected usage. They appear systematically arranged. While individual patterns may have mined from their authors’ messy design experiences, the way they are presented hides any of that uncertainty. Those authors seem to know their stuff!


Recently I’ve learned that some pattern authors were not so certain as their writing suggests. Ralph Johnson, in his [Sugarloaf PLoP 2014 keynote](https://youtu.be/ALxQdnOdYXQ) said that when they wrote Design Patterns, he and his co-authors found the creational, behavioral, and structural categories for their pattern collection rather dubious. They went ahead with them anyways, for lack of any better organizing scheme. In his keynote Johnson proposed a better way to categorize the GoF patterns (core, creational, and peripheral), stating that some patterns were definitely less useful, or peripheral than others 


Likewise, Eric Evans in several talks suggests that the most important patterns in his collection were the Strategic Patterns. If you look at how the patterns in his book are laid out (see Figure 1) there are really two groupings or patterns collections—those concerned with design details for object designs (e.g. Tactical Design Patterns) and those for organizing and understanding the domains in complex software systems (Strategic Design Patterns).  Evans believes that while the Tactical Patterns are useful for object-oriented programming, they aren’t nearly as important as the Strategic Patterns. He regrets that the Strategic Patterns were in the latter part of his lengthy book, as some readers never get that far. He also points out that a missing pattern, Domain Events, which was only hinted at in his book, has become increasingly important, especially with the increased use of CQRS (Command-Query-Response Segregation) and Event-Sourced architectures to implement Domain Driven Design models.


Figure 1. The Domain-Driven Design Patterns are really two collections in one book: Strategic and Tactical Design Patterns


In hindsight, the presentation of these pattern collections seems more tentatively than carefully planned. Had the authors taken time to study how others actually used their patterns, would they have designed better pathways? Or is this something they can see only when looking back on their work?


Perhaps they were really blazing trails instead of constructing pathways.


We can also draw useful analogies between patterns collections and trails. Trails aren’t planned and built; they emerge over time. What exactly is it that makes a trail a trail? Richard Irving Dodge, in his 1876 book *Plains of the Great West*, drawing from his experience as a tracker, defined a trail as a string of “sign” that can be reliably followed. “Sign” refers to the various marks left behind by an animal in its passing—scat, broken branches, spoor, etc. A track is evidence; a mark or a series of marks or “sign” that something that has passed through. A track only becomes a trail when a series of “sign” can be followed. Sign, according to Moor, can be physical, chemical, electronic, or theoretical. An animal might leave “sign” but unless it can be tracked reliably, a series of “sign” doesn’t automatically make it a trail.


Trails are trails because they can be trailed. Moor claims that, “something miraculous happens when a trail is trailed. The inert line is transformed into a legible sign system, which allows animals to lead one another, as if telepathically, across long distances.”


When patterns authors write about what they’ve found to be used in practice, the patterns they present have the potential to be trails that others eagerly follow. But this potential only exists if the authors explain how to move from one “sign”/ pattern / heuristic to the next. I’ve seen scant evidence of this. Patterns maps in books typically don’t describe movement through the patterns. Instead, like rough hand-sketched maps, they suggest only vague connections. Individual patterns seem more like clumps of potentially interesting waypoints, loosely linked or roughly categorized at best. Most authors stop short of laying out waypoints or “sign” in any specific order to follow.
On the other hand, pattern languages, unlike pattern collections, attempt to define one or more sequences of use. Once you add potential sequences, voila! pattern languages seem much more like trails.


I know of few examples of published software design pattern languages. *Object-oriented Reengineering Patterns* by Serge Demeyer, Stéphane Ducasse, and Oscar Nierstrasz is a notable one. Each chapter starts with a pattern map illustrating potential sequences through the patterns in the chapter based on actions (see Figure 2 for the pattern map for Chapter 4). These maps illustrate small trails with branches, loops, and options. For example, to gain an initial understanding of a design, you can start with either a top down or bottom up approach and proceed until you have enough understanding to move on to your next re-engineering task.

Figure 2. Each chapter in *Object-Oriented Reengineering Patterns* is a small language


Unlike physical trails, where we are guided to move in a singular direction, software pattern languages seem more loopy and fragmented. But unlike a physical trail where we are constrained by the physical terrain, software designers can skip over any pattern they don’t find useful or go “off trail” at any point to pick up and apply a useful design heuristic, wherever it is found. It’s hard to skip over a part of a physical trail. It’s only possible when there’s a switchback that you can cut through or a branch. But it is usually those optional stretches away from the main trail and then back again that lead to something really interesting (you don’t want to miss that waterfall simply because it is an extra ¼ mile out of the way).


We software designers often invent (design? hack out?) our own tracks. If we don’t know what to do next, we become way finders, experimenting and looking around for actions that will propel us forward. To me that doesn’t feel like bushwhacking; it just seems expedient. Software designers aren’t constrained to follow a patterns trail exactly as any pattern language author suggests anymore than fluent speakers are constrained to express their thoughts using only the formal grammar defined for their language.


So this is where the pattern languages as trails metaphor breaks down. Software design doesn’t simply proceed from one known waypoint to the next. It’s often more complicated. But sometimes it is much simpler. We aren’t always way finders or followers. Sometimes we are so certain what to do next without consciously following any trail or path or track at all. In that case, the terrain of our software and its design is so familiar to us that we become efficient at just moving through it without much thought. We’re not searching for heuristics so much as taking the next (to us, anyway) obvious step.

## The roles of trailblazers, travellers, and stewards
>“The soul of a trail—its trail-ness—is not bound up in dirt and rocks; it is immaterial, evanescent, as fluid as air. The essence lies in its function: how it continuously evolves to serve the needs of its users.” —Robert Moor

Trails emerge; living useful trails evolve. Wild, ancient trails started as traces—marks, objects, or other indication of the existence or passing of someone or something. Because others followed, some traces over time become tracks—rough ways typically beaten into existence through repeated use rather than consciously constructed. Tracks became trails only when they become followable. And then, with enough following and time and adaptation a trail becomes “alive” with an evolving purpose—it changes and is adapted by its travellers. But this progression isn’t inevitable. Traces peter out. Tracks fade from disuse. Trails become lost, abandoned, or fall into disrepair. Still, each at one point in time had utility and served a purpose.


Like trails, through many uses the rough edges of software patterns get smoothed off. If they seem polished enough, and we have enough of them that are related to each other, we who feel compelled to write them down create patterns collections…hoping others find them useful. But unlike physical trails, which change with use and with the weather and the season, our software patterns, collections, and languages aren’t so easily changed. Our software design patterns are representations—like maps of a trail; they aren’t the trail itself. Consequently, there isn’t a direct feedback loop between recorded patterns and how their users have changed them.


If we were careful enough when we wrote down our patterns we also included the context where we found them to be useful. But the context of those who want to follow our trails, is constantly changing with the type of software being designed, the constraints of the larger ecosystem it is part of, and with the skills and tools at hand. Therein lies a big problem for sustaining the liveliness of software patterns. If we want written descriptions to continue to guide others, to evolve and be ever useful, we need to find ways for users of them to refresh them. And that starts by creating vital feedback loops between software pattern users and their various trail keepers or stewards.

>“We tend to glorify trailblazers…but followers play an equally important role in creating a trail. They shave off unnecessary bends and brush away obstructions; improving the trail with each trip.” —Robert Moor

We in the software patterns community seem to glorify trailblazing patterns authors. A trailblazer formally identifies a trail by creating marks or “blazes” that others can follow. Most likely, a trail existed before it was “blazed.” But the trailblazer, who made the marks, is credited with creating it. But patterns authors claim to not have created their patterns so much as discovered them in existence and documented them. We are a humble lot. But when pattern authors mark what they see, they make it easier for others to follow. Pattern authors also do a great service in pointing out the features of the terrain, e.g. the design context and forces, as other, inexperienced designers may not consciously think of them otherwise. Indeed, this, too, is a form of trailblazing.


Often confounding to pattern newcomers is the fact that solutions to real-world problems are more complex than the stylized ones written about in any particular software pattern. I have used and extended patterns from several different collections on more than one occasion. I remember feeling when my solutions were more complex and nuanced than the patterns described in these books and that I had found clever ways to extend and augment those patterns. A solution that I worked on that represented complex roles and privileges for individuals belonging to multiple organizational structures far exceeded the simple relationships in the Accountability and Accounting patterns described in Fowler’s *Analysis Patterns*.


But I also remember the discomfort of my less pattern savvy colleagues who felt that they hadn’t gotten a pattern “correctly” if we needed to refine or extend it. Only after reviewing our design with Martin Fowler and passing along to my colleagues confirmation that indeed, he thought our problem seemed to warrant a more complex solution, did they feel comfortable with our design.


We can get too hung up on the notion that the initial authors of software patterns, e.g. the trailblazers who blazed more visible trail markers and shored up parts of the trail, making it easier for others to follow, are the best curators of their patterns’ ongoing evolution. Often they are not. Patterns get modified and refined during their application. It’s the pattern users and community of software designers that embrace those heuristics and push them to their limit who discover more useful devices, nuances, modern techniques, and variations.


Unless there is a strong caring community around the original pattern authors, these insights won’t get shared with those who care about sustaining those patterns. Even with feedback, renewed versions of “classic” patterns takes sustained energy and attention to detail and the changing software design scene to keep patterns relevant.


Eric Evans speaks of the revitalization of the DDD community which happened when several DDD leaders introduced and explained the relationships between domains, bounded contexts, and the implementation of domain models using CQRS and Event-Sourced architectures.


I spot some hesitancy for some to update “official” trails mapped out by the original patterns authors; not wanting to step on the toes of those original trailblazers. But those of us who want to preserve trails can and should become trail stewards—volunteering to mend and repair and refine those trails we cherish. What we trail followers need to recognize is that not all trailblazers are alike. While certain trailblazers may not welcome updates, others may gladly seek company, advice, and stewardship help. And some trailblazers may have moved on, having passed through their territory and on to newer ventures. Trail followers have just as much collective ownership of the trails they use as those who initially marked them.

## Fieldnotes on an experiment collecting heuristics
Motivated to share what I’ve learned about heuristics and to stimulate others to share and refine their own and other well-known heuristics that might need refreshing/revisiting, I presented a keynote, Cultivating Your Design Heuristics at the Explore DDD 2017 Conference. I hoped to inspire others to take on a more active role as Domain Driven-Design heuristics stewards. The last sentences of my talk abstract had this challenge:
>“To grow as designers, we need to do more than simply design and implement working software. We need to examine and reflect on our work, put our own spin on the advice of experts, and continue to learn better ways of designing.”

The day after my talk, I got a Twitter direct message from Mathias Verraes, one of the thought leaders in the Domain Driven Design Community. My talk had inspired him to get serious about capturing, recording, and organizing his own heuristics. So we met for a couple of hours at the conference.


I was eager to have a conversation with Mathias and share ideas. Mostly I wanted to practice hunting for heuristics through conversation, as well as gain insights into Mathias’ personal design heuristics for events. Mathias is expert in event-sourced architectures, an alternative to the “traditional” domain-layering architectures (which includes patterns for storing and retrieving and updating Aggregate Roots into repositories), which Eric Evans had written about in his book (see Figure 3).

Figure 3. - A “canonical” representation of the architecture where business domain objects or aggregates are maintained in a database which is accessed through a repository which hides the data store details from the business layer logic.


In a nutshell, instead of storing and updating Aggregate Roots (e.g. complex business domain objects) into databases, with event-sourced architectures, immutable events are stored with just enough information so they can be “replayed” to reconstitute the current state of any Aggregate Root. In essence, an event is a record of what the software has determined to have happened. Whenever work is accomplished in the system, one or more “business level events” are recorded that represent the facts known at the time. Events are generated by a software process as a byproduct of determining what just “happened” and interpreted by interested downstream processes, which can in turn, as a result of processing or interpreting the events they are interested in receiving, generate even more events. Each event is preserved in an event store, along with relevant information about the event. Figure 4 shows a canonical CQRS (Command-Query-Response-Segregation) architecture, one approach to implement event-sourced architectures. It should be noted that although the figure only shows one event store and one read model, there can be multiple event stores (each representing some cumulative state of the system) and different projections or read models designed for specific queries about those events.

Figure 4.  A CQRS Architecture Showing Event Stores


I didn’t know Mathias’ thinking on designing event-sourced architectures. So I wanted to first ask him to explain some fundamentals before sharing his heuristics for what should be published in an event. Throughout our conversation Mathias used as a working example the designs for car rental, finance, and student grading for courses and modules given by instructors (all examples drawn from real systems he had designed).


Mathias quickly rattled off two heuristics, along with examples:
***
*Heuristic:* A Bounded Context should keep its internal details private.

*Heuristic:* Events are records of things that have happened, not things that will happen in the future 
***
For example, an event should be named “a reservation for a car rental has been made” instead of “rent a car” if the customer has just gone online and asked to rent a car. People often confuse what has just happened with real world events that are in the future. When you reserve a car you aren’t actually renting it (not yet). You’ve just reserved it for a future date.


I asked Mathias what he meant by keeping internal details private.


Mathias then shared this example: If you are keeping monetary units in say 10 digits internally in a service, you would only pass out an amount in 2 digits precision because that’s all other consumers of the event outside of the Bounded Context would need. Perhaps there was another heuristic exposed by this example.
***
*Heuristic:* Don’t design message or event contents for specific subscribers to that event.
***
I wanted to understand the implications of this heuristic. So I asked, “So does that mean that you have to know what processes will consume any event in order to design an event record?” The discussion then got a bit more nuanced. Mathias said that you have to understand how events flow around the system/business. Whatever you do, you publish business events, not technical events that are consumed by other processes outside of a particular Bounded Contexts. So yes, you really need to know how business events might be used to accomplish downstream business processes in other Bounded Contexts. Events along with their relevant information, once published are simply streamed out and stored over time to be picked up (or not) by any process that registers interest in that event. So of course the consumer of an event needs to know how to unpack/interpret the information payload of that event.


Distilling what he said, I offered this heuristic.
***
*Heuristic:* When designing an event-sourced architecture understand how events flow around the system/business.
***
Our conversation continued.


I asked, “Who should have the burden of decoding or translating the event payload into the form needed?”

Mathias answered, “the consumer, of course. But the generator of the event cannot ignore the needs of potential consumers. So there might be an agreed upon standard convention for money, for example, is 2 digits precision.”

This led us to conclude we’d uncovered yet another design heuristic. 
***
*Heuristic:* Design agreed upon standard formats for information in business events based on expected usage.
***
And just to poke at an edge case that came to mind as we were talking, I asked, “Well, what happens if a new process needs that extra precision?” Mathias was quick to reply, “Well, maybe it needs to be within the Bounded Context of that process that knows of that 10 digits precision.”

I pushed back, “But what if it doesn’t logically belong in the same Bounded Context?” Which led us to conclude that perhaps there was a competing heuristic that needed to be considered along with the “Design agreed upon standard formats” heuristic.
***
*Heuristic:* When designing a payload for an event don’t lose information/precision. 
***
That led Mathias to restate that while information within a Bounded Context might contain extra precision or information; information that gets passed “outside” a Bounded Context via a Business Event shouldn’t contain “private details.” Our conversation continued for over two hours. I have more pages of heuristics notes and examples that I will only briefly summarize.


Me: How much information should be passed along in an event record?

Mathias: Just the key information about that event so you can “replay” the stream of events and recreate the same results. 
For example, if it is a “payment received event”, you don’t want to pass along all the information about the invoice that was paid. 
This led us to some deep discussion about events and time and that time is really important to understand (and that events can be generated by noticing the passage of time, too).

More heuristics tumbled out.
***
*Heuristic:* If a different actor performs an action it is a different event.
***
For example, it is one thing for a customer to report an accident with the vehicle or to return a car, and another thing for an employee to report an accident or even the car itself if it has telemetry to do so. These are all different kinds of events.
We discussed more heuristics about events. 
***
*Heuristic:* If there are different behaviors downstream, then multiple, different events might be generated from the same process.
***
And this is when Mathias started to draw a representation of his architecture for event streaming and the events that happen over time. He stated that since all events are available to a process, it can find out the “set” of events it is interested in to drive behavior.
***
*Heuristic:* Look for a pattern of events within an event stream to drive system behaviors.
***
For example, you might want to design your system to not send an overdue notice if you’ve recently received payments, however recent is defined by the business. To do that, the overdue notice process might query the event store for payments to find previous events (and check their timestamps) before sending overdue notices.


We also talked about the situation where a customer changes addresses too frequently (say 3x in a single week). Perhaps this detection of events might cause a fraud detection process to be initiated. And even the same stream of events coming in at a different timescale might represent an opportunity initiate different behaviors/processes.
***
*Heuristic:* Consider the timescale when looking for patterns of events. The same set of events over a different time period might be of interest to a different business process.
***
We reluctantly concluded our conversation when we were invited to join the conference’s closing circle. Mathias had written on both sides of a big sheet of paper, sketching ideas as he went. I asked if he wanted to keep the paper. He said no, he knew this by heart as he covers what we had talked about in a three-day workshop he gives. I now wish that I had taken a photo of his scribbling to jog my own memory.







