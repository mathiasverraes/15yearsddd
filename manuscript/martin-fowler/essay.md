# Multiple Canonical Models (by Martin Fowler)


## Multiple Canonical Models

*Adapted from an article published in 2003*

Scratch any large enterprise and you'll usually find some kind of group focused on enterprise-wide conceptual modeling. Most commonly this will be a data management group, occasionally they may be involved in defining enterprise-wide services. They are enterprise-wide because rather than focusing on the efforts of a single application they concentrate on integrating multiple applications.

Most such groups tend to focus on creating a single comprehensive enterprise model. The idea is that if all applications operate based on this single model, then it will be much easier to integrate data across the whole enterprise - thus avoiding stovepipe applications. Much of this thinking follows the shared database approach to enterprise integration - where integration occurs through applications sharing a single logical enterprise-wide database.

A single conceptual model is a tricky beast to work with. For a start it's very hard to do one well - I've run into few people who can build these things. Even when you've built one, it's hard for others to understand. Many times I've run into the complaint that while a model is really good - hardly anyone understands it. This is, I believe, an essential problem. Any large enterprise needs a model that is either very large, or abstract, or both. And largeness and abstractness both imply comprehension difficulties.

These days many integration groups question the shared database approach, instead preferring a messaging based approach to integration. I tend to agree with this view, on the basis that while it's not the best approach in theory, it better recognizes the practical problems of integration - especially the political problems.

One of the interesting consequences of a messaging based approach to integration is that there is no longer a need for a single conceptual model to underpin the integration effort. Talking with my colleague Bill Hegerty I realized that

- You can have several canonical models rather than just one.
- These models may overlap
- Overlaps between models need not share the same structure, although there should be a translation between the parts of models that overlap
- The models need not cover everything that can be represented, they only need to cover everything that needs to be communicated between applications.
- These models can be built through harvesting, rather than planned up-front. As multiple applications communicate pair-wise, you can introduce a canonical model to replace n * n translation paths with n paths translating to the canonical hub.
- The result breaks down the modeling problem, and I believe simplifies it both technically and politically.

So far, however, it seems that the data modeling community is only beginning to catch on to this new world. This is sad because data modelers have a tremendous amount to offer to people building canonical messaging models. Not just are skills not taking part, many also resist this approach because they assert that a single enterprise-wide model is the only proper foundation for integration.

---

## Bounded Contexts

*Adapted from an article published in 2014*

Bounded Context is a central pattern in Domain-Driven Design. It is the focus of DDD's strategic design section which is all about dealing with large models and teams. DDD deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships.

![A diagram of Context Map](images/martin-fowler/contextmap.png)

DDD is about designing software based on models of the underlying domain. A model acts as a [UbiquitousLanguage](https://martinfowler.com/bliki/UbiquitousLanguage.html) to help communication between software developers and domain experts. It also acts as the conceptual foundation for the design of the software itself - how it's broken down into objects or functions. To be effective, a model needs to be unified - that is to be internally consistent so that there are no contradictions within it.

As you try to model a larger domain, it gets progressively harder to build a single unified model. Different groups of people will use subtly different vocabularies in different parts of a large organization. The precision of modeling rapidly runs into this, often leading to a lot of confusion. Typically this confusion focuses on the central concepts of the domain. Early in my career I worked with a electricity utility - here the word "meter" meant subtly different things to different parts of the organization: was it the connection between the grid and a location, the grid and a customer, the physical meter itself (which could be replaced if faulty). These subtle [polysemes](http://en.wikipedia.org/wiki/Polysemy) could be smoothed over in conversation but not in the precise world of computers. Time and time again I see this confusion recur with polysemes like "Customer" and "Product".

In those younger days we were advised to build a unified model of the entire business, but DDD recognizes that we've learned that "total unification of the domain model for a large system will not be feasible or cost-effective" [1]. So instead DDD divides up a large system into Bounded Contexts, each of which can have a unified model - essentially a way of structuring multiple canonical models.

Bounded Contexts have both unrelated concepts (such as a support ticket only existing in a customer support context) but also share concepts (such as products and customers). Different contexts may have completely different models of common concepts with mechanisms to map between these polysemic concepts for integration. Several DDD patterns explore alternative relationships between contexts.

Various factors draw boundaries between contexts. Usually the dominant one is human culture, since models act as Ubiquitous Language, you need a different model when the language changes. You also find multiple contexts within the same domain context, such as the separation between in-memory and relational database models in a single application. This boundary is set by the different way we represent models.

DDD's strategic design goes on to describe a variety of ways that you have relationships between Bounded Contexts. It's usually worthwhile to depict these using a context map.

## Further Reading

- The canonical source for DDD is [Eric Evans's book](https://amzn.to/2AUG3q0). It isn't the easiest read in the software literature, but it's one of those books that amply repays a substantial investment. Bounded Context opens part IV (Strategic Design).

- [Vaughn Vernon's Implementing Domain-Driven Design](https://amzn.to/2MwG58S) focuses on strategic design from the outset. Chapter 2 talks in detail about how a domain is divided into Bounded Contexts and Chapter 3 is the best source on drawing context maps.

- I love software books that are both old and still-relevant. One of my favorite such books is [William Kent's Data and Reality](https://amzn.to/2vutD3c). I still remember his short description of the polyseme of Oil Wells.

- Eric Evans describes how an explicit use of a bounded context can allow teams to graft new functionality in legacy systems using a [bubble context](http://domainlanguage.com/wp-content/uploads/2016/04/GettingStartedWithDDDWhenSurroundedByLegacySystemsV1.pdf). The example illustrates how related Bounded Contexts have similar yet distinct models and how you can map between them.
