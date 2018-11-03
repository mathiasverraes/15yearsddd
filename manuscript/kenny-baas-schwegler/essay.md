# Model Exploration Whirlpool (by Kenny Baas-Schwegler)
#### with EventStorming and Example Mapping

## Introduction
People often ask for more concrete guidance on how to explore models, especially in an Agile or Lean setting. The model exploration whirlpool is Eric Evans attempt to capture such advice in writing. It is not a development process, but a process that fits in most development processes. The central theme revolving the process is to keep challenging the model. While the process itself for most is straightforward and easy to understand, there are not many concrete examples to find on how to do such a model exploration whirlpool. Most people when starting to use Domain-driven design (DDD) are looking for these practical examples. In this article, I will tell you my story of how I used the model exploration whirlpool by combining EventStorming, a technique that came from the DDD community, and Example Mapping, a technique from Behaviour Driven Development (BDD) community.

## Harvest and document
We start model exploration with harvesting and documenting the current state. If you don't have a current state and going green field, don't worry we will get to that part. The primary goals are to collect reference scenarios, capture bits of the model and then leave most ideas behind. The starting point for this stage can be several of the following; A constraint formed out of a big picture EventStorming; A new project; or just a user story on the backlog. As long as there is a storyline to tell, it is a good starting point. 
Two of my favourite tools to use here are EventStorming and Example Mapping. It is essential for the success of the workshop to know who the right people are to invite. These are the people who know the domain, the domain experts. We would want to be inclusive as possible, but there are exceptions. It is vital that we create a safe place in where knowledge can flow freely, a great facilitator can do miracles, but there are limits. People who are toxic are killing for a productive workshop, so we might want to decide to leave such a person out. The problem can be is that this person has a lot of information. It is perhaps wise at this stage to talk to this person before such a workshop and see if we can get some information out, or even better but harder, change his toxic behaviour so that the person can join the workshop.

### The workshop
One important thing here is to find enough modelling space, preferably infinite space (if ever!). I look for rooms with at least a wall of 8 meters long where I can put a whitepaper on, and it definitely needs a whiteboard. Now we can start capturing the current state by doing a process EventStorm. We give the participant some orange stickies and a marker. We ask them to write down Domain Events for the current state of the system and put them on the white paper in order of time. There will be a lot of chaos, so be sure to do some expectation management and explain that eventually, we will structure it.

### Tell a story
When everyone wrote down his or hers Domain Events, it is time to tell a story. Let the attendees enforce the timeline now by making the story consistent. Remove duplicate events, but make sure they are in fact duplicates. Often people assume a Domain Event is the same even but isn't. Be concrete and specific. At this point, expect to find different opinions about the expertise. Mark these with a bright pink sticky called a hotspot, something that is noticeable from a distance. 

### Make the implicit, explicit!
The core of visual meetings like EventStorming is that we discuss only explicit and visible things. There is just so much knowledge we can capture in Domain Events and hotspots; we can capture more types of knowledge with other colours. The standard EventStorming colours are (but make your legend with the colours you have available):
Blue: Action/Command
Long Pink: System
Long Lilac: Policy/Eventual Business Constraint
Green: Information
Every other knowledge
The basic flow will look like this, but the key point here is to use what we need. If we don't know, try and follow this flow.

### Bias blind spot
Now that we think the story is complete we want to bring in Example Mapping. Most of the time people will now believe that bringing in another tool is doing waste. We got our story visualised right? The problem is that everyone is subject to cognitive bias, especially when we get information overload. We notice things already primed in memory or repeated often, which are context effect and attentional bias. We are also drawn to details that confirm our own existing beliefs, the observer effect and the confirmation bias. Especially noticing flaws in other more easily than yourself, the bias blind spot, is dangerous during our exploring of the domain. To battle these we need to use different viewpoints, other tools.

Example mapping helps, because it focusses more on examples or scenario's, then on events that happen. Start the discovery with writing down examples and scenarios in the form of friends episodes, the one where. Think out of the box, and see where these examples affect the current EventStorm. Is it a gap in the current system, or is it a gap in knowledge which is futile to go on, mark it with hotspots, make it explicit! Now at this point, with the people in the room, we probably harvest enough insight of the current state.  This first part of the workshop will take about two to three hours, a minor investment to the knowledge that is gain.