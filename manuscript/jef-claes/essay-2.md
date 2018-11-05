# Not About the UI and the Database (by Jef Claes)

_Published on jefclaes.be 2014-06-01_

When you ask an outsider which components an average application consists of, he will most likely be able to identify the user interface and the database. He will also recognize that there is something in between that takes the input from the user interface, applies some logic and persists the result in the database.

![1](images/jef-claes/2/1.png)

In the past, trying to make sense of what goes on the middle, we started - with the best intentions - layering things. Each layer had its own responsibility and would build upon previous layers. Although there was a layer for business logic, we never really succeeded in capturing the essence. In the end we would still be orchestrating database calls, but now we would be forced to go through a bunch of indirections in the form of anemic layers and objects.

![2](images/jef-claes/2/2.png)

Some people saw these designs for what they were, broke free and started optimizing for the shortest path - from user interface to database with the least amount of effort. By aiming to serve the common denominator and by putting their trust in dark magic, frameworks popped up that would allow you to slap together an application in a matter of hours.

![3](images/jef-claes/2/3.png)

The problem with these frameworks is that they leave you with very little room for your own, and you often end up jumping through hoops when you need to deviate from the path carved out for you.

![4](images/jef-claes/2/4.png)

That's not the only problem though - applications are a lot more than a user interface and a database. What lives between those two is more than a technical necessity - it's a place where you get to build a model of the problem you are solving. The model gives you an opportunity to learn from and to communicate with domain experts, peers and users. And that's exactly where most businesses make the difference, not by having a fancy user interface or a carefully designed database schema, but by really understanding and by being absorbed by the problem they are solving. It's the user interface and the database that are the necessary evil we bring upon ourselves by solving problems using computers.

The state that lives in your database is a side effect - the result of the model's behavior. The user interface tries to make it as easy as possible for users to drive and use the model.

![5](images/jef-claes/2/5.png)

Although the user interface and the database are important, it's the model that is the heart and soul of your application.
