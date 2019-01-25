# To DDD or not to DDD... What to do if your domain is boring? — Weronika Łabaj

I've heard countless times that DDD should ONLY be applied to complex, interesting domains. Even experts I deeply admire say that, so it must be true, right?

But I've never heard anybody explain what exactly makes a domain interesting or complex enough. Specifically, what makes it interesting or complex enough for the purpose of DDDifying it. 

I think we've been asking the wrong question and this tweet by @DDD Borat summarizes my thinking perfectly:

![A bird model for a physicist (by DDD Borat)](images/weronika-labaj/ddd_borat.png)

Before I explain what I mean exactly, let's have a quick look at two situations that shaped my opinion on the subject.

## Example 1: Anemic domain model. Boring, Boring, Boring Line of Business App (BBBLOBA).

A few years ago I worked on an e-commerce system. We've basically implemented everything an online store does, starting from displaying catalogs, through managing promotions, calculating current prices, checkout process, through emails, payments integrations, to all the backend stuff that customers never see, like refunds or shipments integration.

The business logic was randomly divided between controllers, data access classes and stored procedures. There was no business logic layer whatsoever when I started there.

One day I was particularly frustrated. Looking at yet another property bag which was proudly (though inaccurately) called our "domain entity", I mumbled something about Anemic Domain Model. My colleague overheard it. He sighed: "Yep, no wonder we have an anemic domain model here", he said. "There's no interesting business logic. That domain is just soooo boring."

I wasn't sure what to say. I've just spent a whole week investigating how refunds are calculated. I found a bug, which was rejected by our QA saying "It's too complicated, I'm not raising it". If that wasn't an interesting piece of business logic, then I have no idea what else it was. So I only nodded my head in faked agreement and went back to work.

## Example 2: Domain crunching applied. Boring, Boring, Boring Pet Project.

A while ago together with my boyfriend we got really pissed off with the mess which is called our personal finance. We simply had no idea where exactly our money went, how much we made and how much we spent. 

We used Excel before, but that didn't seem good enough anymore. Our finances got more complicated over time. Also our expectations got higher, because after a few years of tracking expenses, we knew what we wanted out of the app. So we did research, I checked dozens of apps and none of them fit our criteria. We could hack them to fit our needs and do some calculations outside of the app (probably in Excel). 

Instead we did what any programmer would do in such a situation - we decided to write our own.

Now this surely is the most boring domain one could imagine, right? Apart from maybe a TODO list, it's the most popular pet project ever. Every programmer at some point rolles out their own version of the expense tracker.

Over we've learned a lot about that domain.

The first insight was that in fact we have two main parts in our app, which are to large extent independent. Tracking and analyzing money. That fact impacted our model in significant way.

For example accounts are very useful for tracking. I can compare the actual total of one out of our 11 accounts and the data in the app. If some entries are missing, it's helpful to know what kind of transaction it was. It narrows down the search in the online banking systems and helps with remembering where I last spent cash. Accounts are perfect for this purpose.

On the other hand I don't care about accounts at the analysis stage. I don't care if the specific payment was made from my personal account, our joint account, or my boyfriends wallet. Consequently, why in the world would I filter my expenses by account in reports? It gives me no actionable insights whatsoever. Adding such a feature would be a waste of time.

You might think "Isn't it obvious? What's the big deal?". This is exactly what shows that we're on the right track with modeling our domain. Afterwards it seems like the most obvious thing under the sun. But I can assure you it wasn't that obvious when we started. Plus, most apps DO reports by account. Don't ask me why would anybody use this. I have no idea, because I wouldn't.

Then we hit our first problem. I'm self-employed, so I pay my own taxes and health insurance. It's not really an expense, in the sense that I can't do much to make it lower. So from the perspective of optimizing expenses it was only a noise in reports. Yet, I wanted to track it in some way. 

At first we added a flag which indicated whether the specific expense should be included in analysis. But after a while we've realized we have a missing concept here - an income cost. We have other expenses that shouldn't be included in reports, but tracking my income costs on its own is actually very useful information! Making this concept explicit made our code easier and less error-prone.

The next challenge came from my boyfriend. He does a lot of business trips. He covers expenses during his trips himself, and then his employer reimburses the expenses in the next month's salary. He goes mainly to countries more expensive than Poland, so those expenses are relatively high. They completely ruined our analysis, and made tracking all expenses challenging. We still wanted to track those in the app, so we don't forget to check if the money was returned, but those weren't just normal expenses like groceries. That lead us to discovering another new concept - reimbursable transactions.

Since I occasionally lend money to family or friends we thought about explicitly modelling loans too. After giving it some thought we decided that using the same reimbursable transactions for business trips and loans is good enough. If we ever need more detailed distinctions between those two types of transactions, we can adjust our model.

We've made many more discoveries like those described above. We used the app, noticed that something feels wrong, discussed it and refined our model. With each new discovery, our model got cleaner and made more sense. Looking back we were surprised we didn't come up with all of this from the very beginning. It looks so obvious looking back!

## Back to the DDD Borat

If you think about this, an e-commerce platform is way more complex and interesting system than a personal finance app. Or is it?

I think we've been asking the wrong question here. It's not about the domain per se. It's not that one domain is more interesting or more complex than the other. Being interesting is not an intrinsic characteristic of a particular domain.

What makes a particular domain interesting are problems you are solving.

In many cases it doesn't make sense to go with your "domain crunching" very deep. If you can get away with CRUD, then by all means, do CRUD. If you're a physicist then a bird is a bird is a bird, that level of abstraction would do just fine. It wouldn't work that well for a biologist though.

The other thing that makes a particular domain interesting is you.

Can you notice when your model is not good enough anymore? Do you know when it's time for a re-modeling session? Do you ever talk to your domain experts using their language? Are you truly interested in their problems and how to best solve them?

If not then no domain would be "interesting enough" to justify using DDD.

## No excuses

In our case applying DDD concepts to the pet project really paid off. The app is easy to use, we make fewer mistakes using it than in the beginning. When it was a simple CRUD app, I messed something up at least few times a week, because I forgot what flags to set in what situation. Fixing my mistakes could take us anything between 10 min. to 1 hr. Now each concept is modeled explicitly and I have no doubts how to enter all transactions, even when I'm exceptionally tired. And we got incredibly useful insights from all this data, which impacted our life in many ways.

So don't let the popular myth hold you back. You can apply the so-called "strategic design" principles even in your pet project starting today.