---
layout: post
title: Develop on cadence!
subtitle: reflections on agile software development
bigimg: /img/austin-neill-163306-unsplash.png
tags: [software engineering, test automation, microservice]
---

I work as a freelancer in technical testing, so software quality is something very dear to me. Agile software development tremendously helps with that. But discussions of Agile software development often drift towards development methodologies like Scrum vs. Kanban. I think this discussion is healthy but sometimes misses the point since there is already existing prove that both work but have strength and weaknesses, too. To me Agile has a much more fundamental impact on software projects. In this post I want to discuss two topics that I experienced in the past as key Agile pillars especially for avoiding the Big-Bang software development mode.


## Develop on cadence release on demand

In the context of software quality one of the topics I often discuss with managers and coworkers is communication. My consistent observation from taking part in many projects is that if a project has quality issues the root cause is communication - each and every time. One of my managers once said: "they (the DEVs) do not talk to him because they are afraid of misunderstandings". While this might sound a little bit sad, we actually had a big laugh. In case of a "late" project things like this are a common symptom. People focus on finishing their own tasks and often miss out on communicating important information to others. In this situation if the communication is not already "hard-wired" into the development process, things tend to get worse. In my opinion this concerns one very important key aspect of Agile software development.

Sometimes a project carries all the insignia for agile development but is in reality working towards a big event in the near future like a public go live (Big-Bang). I certainly understand that a company needs to introduce a product to the market as a big marketing event and does not want to release an unfinished product. Therefore it is crucial for success to separate development processes and release processes. It is necessary to split the Big-Bang goal into smaller manageable steps (i.e. releases). It is best also to introduce a recurring rhythm for the smaller development cycles (i.e. sprints) - I like the term cadence to express this phenomenon. Having a cadence makes it easy for everybody to understand what is going on because the current cycle is very similar in structure to the last one - and the one before (think release cycle of Linux distributions). So project communication can focus on the *why* and *what* aspects - which is way more efficient over planning and communicating *how* each an every step needs to be done. Of cause it all depends the circumstances. Three people might easily manage to communicate everything that is going on - but 20? - or 50? How about 100?

The following article gives an excellent introduction into the develop on cadence topic:
http://scaledagileframework.com/develop-on-cadence-release-on-demand/

In nature almost all processes follow a rhythm - so to humans the cadence process concept is a "hard-wired" approach to do things. The following graphic shows some of these processes to help you to get the idea of what I am talking about.

![a typical reflow temperature profile](/media/develop_on_cadence/rhythm_in_nature.png){: width=1000}

In the context of short development cycles regression test automation really shines because it helps to quickly identify anomalies. If a cadence is established, test automation helps to keep the information flowing within the project team.


## Smaller Development Units (i.e. Microservice Architecture)

Avoiding Big-Bang has another dimension that unfortunately in the context of software development processes is sometimes overlooked. Often it makes sense to split a complex software system into smaller & better manageable pieces (thinking divide and conquer). Easier said than done... Since in practice this is probably going to be the most difficult thing to achieve. The topic of smaller development units touches so many different responsibilities in a project organization like requirements, architecture, development, release management, quality assurance, operations. Reducing complexity and gaining efficiency and effectiveness is obviously important for all stakeholders but to reach consensus can be challenging. Our industry came up with an en vogue approach to this called Microservice Architecture. I believe a successful approach will smoothen the way to reach consensus among project stakeholders.

But as always it is necessary to pick the right tool for the the job. Microservice Architectures come at a cost and might not be the right approach for every situation. Microservice Architectures also face their own challenges when dealing with the complexity. Most important from my perspective is to get the domain modeling right from the beginning. Good for us as an industry, that we already have a solid foundation on how to do this. If you are interested in how to tailor the services right, start by reading the blue book (on Domain Driven Design). In addition I find the CQRS concept extremely helpful in making the DDD concepts actionable.

Regarding the software development "machinery" many aspects are "connected". Unfortunately we do not deal with a big collection of unrelated methods. If one part is moved, this usually impacts other parts. This works in both ways. Working on smaller development units make it possible to work with smaller teams. This also makes it possible to increase transparency on responsibilities. As we all know it is way easier to improve Agile software development capabilities with smaller teams.

When thinking about Microservice Architecture it is necessary to think about testing, too. Compared to "untestable" monoliths, a Microservice is way easier to test automatically. But in terms of quality assurance Microservice Architectures are creating new challenges, too. I plan to write some short articles about that in the upcoming months.


Best,
Mark

## Resources

* [Big-Bang](https://lameguy.wordpress.com/2013/05/29/the-big-bang-software-development-lifecycle-model/)
* [Cadence](http://scaledagileframework.com/develop-on-cadence-release-on-demand/)
* [Microservices](http://www.amazon.com/Building-Microservices-Sam-Newman/dp/1491950358/)
* [RESTful Services](http://www.amazon.com/gp/product/B00890OBFI)
* [Microservices](http://martinfowler.com/microservices/)
* [Testing Microservices](http://martinfowler.com/articles/microservice-testing/)
* [Domain Driven Design](http://dddcommunity.org/book/evans_2003/)
* [CQRS](http://martinfowler.com/bliki/CQRS.html)
