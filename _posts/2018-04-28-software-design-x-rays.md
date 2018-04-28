---
layout: post
title: Book review "Software Design X-Rays"
subtitle: Adam Tornhill, 2018
bigimg: /img/ricardo-resende-437822-unsplash.png
tags: [book review, metrics, visualization, software engineering, test automation]
---

"Software Design X-Rays" is Adam Tornhills 2nd book on the topic of "statistical code analysis" which expands on his previous book. I think about the book as a pragmatic guide book on overcoming learning plateaus in software development organizations. I wish it were required reading for decision makers in such organizations.

Adam motivates us to up-our-game with "better decision making" and argues that software often is "more expensive to maintain than it should be". He opens up a feasible road to continuous efficient data driven software maintenance. The book describes methods to get a holistic overview on your codebase and to prioritize improvements.

Part I of the book describes **technical debt** as a metaphor developers use to explain the need for refactoring. It is also used to communicate technical trade-offs to business people ("we release our software faster at the expense of future costs").

Adam gives some accounts on projects which "mistake organizational problems for technical issues".

The book provides an exhaustive explanation on the averse impact of parallel work on quality which is caused by the following organizational factors:

- **structure of development organization**
- defect risk increases with the **number of developers** who are working on a particular section of the codebase

Adam demonstrates how to mine a git version (commit) history for information to:

- find code with the highest interest rate
- measure architectural fit for code evolvement
- find productivity bottlenecks (i.e. multiple teams working on the same code)

Mining the git version history provides us with time dimension & social data.


Part II expands on how the **change frequency** follows a power law distribution (change frequency is defined as "how often a file occurs in the git changelog"). We should consequently focus our code improvement initiative on areas where we find high numbers.

Adam defines **Hotspots** as complicated code that has been worked on often. He suggests to use:

- the change frequency as proxy for **interest rate**
- and "lines of code" as a simple measure of **code complexity**

Adams demonstrates interactive hotspot visualization using enclosure diagrams and tree maps.


In Part III Adam raises the question of "how do we know a software design is any good?". He describes **change coupling** as "files that are changed within the same commit" and gives an interesting definition of **social loafing**.


The book contains exhaustive examples using popular open source software repositories hosted on Github. With this the reader is able to reproduce the analysis and to familiarize himself with the methods and tools. On top of all that the book is accompanied with exercises, a website, and a user-forum.

I know Adams work (in the form of books, open source contributions and conference talks) for a few years now and I admire him for his enthusiasm and persistence in the field of "statistical code analysis and visualization of code quality". His newest book is his best work so far and I very much enjoyed reading it. I am looking forward to put his suggestions to work.


I hope this book review is helpful to you.

All the best, Mark


## Resources

* [Software Design X-Rays](https://pragprog.com/book/atevol/software-design-x-rays)
* [Repositories used in the book](https://github.com/SoftwareDesignXRays)
* [Discussion Forum](https://forums.pragprog.com/forums/472)
