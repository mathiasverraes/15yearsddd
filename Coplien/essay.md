# DDD — The Misunderstood Mantra

Eric, it is a great honor and pleasure that I would find myself in the company of those invited to address you on the 15th anniversary of your _magnum opus_. I too, have been with this process for 15 years, and have watched as both of our ideas have grown. Meeting you at _DDD Europe_ was a highlight for me and was my first opportunity to learn from you first-hand. I still yearn for us to continue that process, and hope we will meet face-to-face again soon, In the mean time, this is like a letter to you that primes the pump for those discussions. I offer these ideas with the greatest rexpect and great expectations of what we'll learn together next.

## Foreword

When I spoke at DDD Europe in 2016, Eric Evans and I commisterated that few people really understand Domain-Driven Design (DDD). It fits the old joke about teenage sex: everybody is talking about it and wants to do it, very few are really doing it, and those that are are doing it badly. Even _I_ find myself scratching my head about it, and in talking to Eric, even _he_ would write the book differently today than when Addison-Wesley asked me to review it back in December 2002.

These reflections mark one perspective on fifteen years of the history of these ideas. Maybe fifteen years is too early to assess a work's place in history; that will take another ten years, at least, I think. But perhaps my current reflections can both give Eric pride in what he has accomplished and challenge him, along with his colleagues, to add new thoughts and insights to the existing base. Much of what I say here, I have no doubt that Eric already has on his mind. If so, so much the better.

## First Impressions
One of the first things that struck me about Eric's book was that he wasn't just another fundamentalist of object-oriented programming. A domain view, particularly in design, 

The most important contribution that Eric has made, in my opinion, is to raise awareness of what he calls the _ubiquitous language_. Though it is not likely ubiquitous and is certiainly not a language, such a collection of words grounds the dialectic from which great design emerges.

But two things bothered me a bit about the book. One was it didn't evoke any of the massive domain analysis literature. In the canon of computer science domains delineate areas of focus or knowledge both in the application and solution sectors of the business. It takes good analysis to find domains that are resilient under program evolution, and the book wasn't attientive to that — though the area is well-trodden. Maybe I invested a bit of my ego in this perspective because of my own work in this area on Multi-Paradigm Design from four years earlier, which is a discipline way of doing what one might well call domain-driven design. More broadly, it

A broader movement... Martin Fowler had taken the time-honored notion of domain-specific languages (DSLs, a.k.a application-oriented languages) and started using it in the sense of conventions embeeded in a program of an existing general-purpose language. There is a kernel of insight behind this to the degree that well-chosen identifiers in a nicely structured language makes the code easier to understand. Still, it's about more than the identifiers, as language is about how we structure the relationships between the words. Even most modern programming languages trace their syntax back to FORTRANB (declation, assignment) and the basic types and semantics of the popular languages are still the algebraic operators. While computing was originally about playing with numbers, we've come a long way, and true DSLs go beyond a mere vocabulary to a true language. Languages have not only syntax, but semantics — and some of the most powerful semantics of a language lie in its idiomatic constructs.

## A section

### A subsection

Some more text. An image:

![This is the Image Caption](images/ddd.jpg)

## Reflections
### First Impressions
I  spoke above of my f´rurstation in not being able to find a theoretic grounding for DDD ideas. It brings to mind a radical proposition: Perhaps, in fact, there is no theoretical grounding to program structure, any more than there is a formal grounding for structuring a building. Sure, a building must stand, and a program must compile and link, but those are more engineering concerns that concerns of science. Even from an empirical perspective it is difficult to tease out theories and principles of good design. And the book _does_ underscore those that we agree about: separation of concerns, attentiveness to APIs.

This rasies a question about whether there is a seperate, viable view of programming-as-craft that breaks with software engineering tradition. I for one hold many softrware engineering platitudes in minor contempt, but perhaps I should join Eric and encourage colleagues to take this disdain even further. Eric's book is a strange book in that, at first glance, it treats topics in the neighborhood of software engineering — most notably, those tried-and-true universals I mentioned above. Both the software engineering literature and Eric's book lack credible grounding for their core ideas, but that doesn't mean the ideas are wrong. And it's unlikely in either case that we will find universals.

In some way I may have fallen into the trap in the same way that we criticize the fundamentalists of object-orientation, top-down design, or waterfall. We have precious little evidence that any of them "work" or not. Waterfall put us on the moon. For example, I can view DDD as what formally is called a _single hierarchy system_. DDD seems to blur coding-time and run-time concepts (a good thing), but there is one perspective and philosophy that stands behind a single structure of bounded contexts. The problem is that they are bounded. Real boundaries rarely exist in the real world. The accounting department and the UX designers don't communicate through well-defined memos and protocols, or even through documents or well-structured meetings, but may exchange the most crucial market needs around the coffee machine, If there protocol is not well-delineated, the protocol of their software artifacts should be equally porous. 

## Bring Back Analysis
Programming languages and their design methods bring little insight into end-user needs, except in the case of domain-specific language.

## By, of, and for the people
I went to a workshop session at the conference where people were talking about software that helped in the maintenance of factory floor machinery. I decided to apply an old test. I sat and quietly listened to their conversation and observed how long it would take for me to find out what business they were in, They were discussing their ubiquitous language, so I thought: This should be easy, I listened. The talked about *entities* (which I figured out were things like machines) with *components* (motors, belts, bearing assemblies) and *associations* (pipes, tubes, and wires connecting the machines) and so many other nerd-centric concepts that I eventually had to ask what these machines actually built. But _motors_, _wires_, and specifie _machines_ were menitoned only in passing as though such use would somehow sully or corrup design understanding. It was design without analysls.

Several months later I would travel to China to serve a client that wanted advice on DDD. They told me they had contacted Eric but that Eric really didn't want to travel to China; besides, he had written a book that conveyed enough of his knowledge that he didn't have to be there in person. I sat through hours of PowerPoint presentations of UML diagrams of design: classes, class hierarchies, and associations. Most of the workers were 20-somethings with a few months or, occasionally, a few years of experience. There had been no concerted effort to canvass the market, to make a domain model (i.e., an enumeration of the business domains and an understanding of their relationships). They could not tell me what problem they were solving. It was nerd heaven.

To make anallysis work means mixing with the hoi-polloi: of getting one's fingers dirty and understanding the non-hierarchical messiness of the real world. DDD structure is a hierarchy (or, at best, a directed acyclic graph) with perfect symmetry. Its symmetry gives it elegance, and that elegance appeals to the analytical mind. Our mind uses the approximate symmetry of nature to cheat how memory works, to save energy: when I meet you., my mind stores away an image of only half your face. Yet if you carefully analyze a picture of yourself, you'll find you're not symmetric. (Take a picture of your face, straight on; make two copies, and cut each copy into perfect halves, right down the nose. Put the halves together in various ways to see the many versions of You.) Yet architect Christopher Alexander reminds us that beauty owes to the breaking of symmetry and to harmonizing with the inevitable imperfections of nature. Many, such as Jef Raskin (_Humane Interfaces_), admonish us to create software tolerant of human frailty and errors.

## Mental Models
One negative, to me, is that DDD talks very little about people. Most software today interacts with an end user, and it's crucilal that the underlying software structure, the elements of the human interface, and the end-user mental model be well-aligned. DDD seems like the nerds' revenge, sitting inside the machine, unbothered by human beings.

If the mental model could steer or more directly drive how we create bounded contexts, I think we would end with systems that have fewer bugs, that evolve better, and that are easier to understand.


## Break the Symmetry
DCi. I spoke of it at the conference.

Eric's book often uses patterns as expository structures. This is one case where I believe the theory could be priceless in moving to the next stage, Pattern theory is all about interaction between and not-separateness of the things we create. Alexander himself uses the phrase "not-separateness" often, and is known for his essay "A City is Not a Tree" that decries urban plannin based on delineated neighborhoods — their bounded contexts. Patterns go beyond DCI in that DCI only breaks two (or maybe three) dimensions of symmetry. They are multitude. The designer who ignores them will produce an inhmane system.

Many idiomatic language constructs are a form of symmetry breaking. Copying an array in C, a novice would do like this:

char array1[10], array2[10];
. . .
for (int i = 0; i < 10; i++) {
   array1[i] = array2[1];
}

But that is just syntax and semantics compliant with (symmetric to) the canonical grammar of the language., If we mix several linngistic constructs, we get:

char array1[10], array2[10];
. . .
char *cp1 = array1, *cp2 = array2;
while (*cp1++ = @cp2++);

True richness of exoressiion comes in concept overlap. For example, in flight reservations, there is a´high overlap between routes and XXX.


## Domain Specific Languages
Make the ubiquitous language more ubiquitous. S for statisticians or Excel or PowerPoint.


## A Taxonomy of Theory and Heuristics
Too often comouter scientists seek overly deeo rationalizations or overly formal reasons for their code. We can analyze user needs to death. But as Freud says, sometimes a cigar is just a cigar.

Sometimes, disjoint bounded contexts are just the ticket. While nothing in the universe is perfectly separate from anything else, somtimes the separation is good enough that each concept can have its own self-contained entity. There is a time and place for such separations, perhaps at the grossest llevel of scale (separating the missle navigation software from the program that controls the hydraulics of the radar antenna) and the finest (a String is a pretty high-integrity concept.)

Yet things are messy in between, and the symmetry breaks. We need both heuristics and design formalisms to decide when to create new entities and when to use more sophisticated approaches such as DCI. Sometimes culture wins out and what is in reality an entangled concept deserves its own identity because of how it matches human mental models. Perhaps such situations should cause us to cast Occam's Razor aside for the sake of pragmatics abd the power of software maintainability that comes with comprehension. A true story is useless if it cannot be understood, and even untrue stories (fables, myths) convey great power.


See https://leanpub.com/help/manual#leanpub-auto-markdown-the-easiest-way-to-format-your-text-for-e-publishing for more about formatting.
