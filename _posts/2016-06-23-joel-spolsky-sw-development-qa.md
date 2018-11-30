---
layout: post
title: Software Development Q&A
subtitle: Joel Spolsky on software development
bigimg: /img/marek-szturc-593635-unsplash.png
tags: [software engineering, test automation]
---

Today I had the chance to meet with Joel Spolsky at a Q&A event. Joel is the CEO of Stackoverflow and maintains an impressive track record as founder in the NY startup community. Given his unique background of being a successful founder with tons of software development experience, Joel has something to say on what works in software development and testing. 

I tried to preserve the gist of this great event since I believe it is much more than just a collection of anecdotes. To me it outlines a framework for a "dashboard" view on managing software development projects.


## Rewriting code

Amongst many things Joel is infamous for his 2000 blog post on "things you should never do". He called a code rewrite "the single worst strategic mistake". Being a computer system migration buff I had to ask him about it.

* It is ok to rewrite small parts / one thing at a time
* Developers are bad judges on code quality. They often miss how much knowledge is contained in the code.
* Rewriting a system usually  means to recreate the very same thing. It takes time and resources and you usually end up with code of similar complexity.
* Sometimes technology changes require a rewrite.
* Sometimes it is necessary to rebuild things from scratch because the world has changed.


## Software inventory

Joel makes an excellent argument by comparing "software inventory" to inventory cost in manufacturing.

* If you carry bug-fixes around without releasing them, then nobody can benefit from the fixes - they are piling up!
* The kanban board helps to identify situations when things are piling up.


## Defects

Joel told us about three dimensions of defects:

* how long the defect lasts
* severity
* how many people are impacted

Often it is possible to reduce the impact at least in one dimension. For example:

* Use CI / CD to rollout fixes quickly
* Severity: provide a workaround
* Some organizations use the following: First they introduce a new release to limited amount of users. If a defect appears they rollback and fix it. In this way they make sure a release is good before rollout to the whole population. The limited group might be identified as friendly users, employees etc.


## Technical debt

We talked a lot about technical debt.

* Many times you get away with it!
* In case the product fails you do not have to pay up the debt
* If the product is successful you have kind of a "luxury problem"

Joel calls it "technical leverage":

* Businesses use debt as a tool to build something with money that is not theirs.
* In software development we can use it in a similar way.

Sometimes developers strive for perfect code. There are different schools and one might follow the SOLID principle. A solution that would take a couple lines of code is split into 47 files and classes. Often something like this leads to over-engineered and complicated code that is difficult to understand and maintain unless someone explains its architecture. It is often better to accept that perfect code does not exist. I personally prefer simple solutions that work over complicated ones.


## TDD (Test Driven Development)

Whether TDD makes sense depends on the task. Joel argues that TDD makes sense for text-based tools like parts of an OS, compiler, backends, etc. It does not make sense as soon as it has a GUI.

In my book this is another great argument for the test-scope-pyramid.

In this regard Joel cites Geoffrey Moore "Core vs. Context". **Core** adds value to your products like for example a search engine. Basically everything that gives you a competitive advantage. **Context** is called everything else you need to do like for example payroll.

This also corresponds with risk based software testing where you distribute your testing efforts unevenly between low risk and high risk areas.


## General tips and practices

We asked Joel a lot about tips and practices. A few things I recall:

* Try to limit dependencies (Open Source, Saas) or at least actively manage them e.g. by writing your own tests or by maintaining your own local package cache / repository.
* Software development moved from chemistry to biology. Sometimes it gets sick for example if a lookup takes longer than expected or Github is down.
* Assign support costs and development costs to the same budget. In this way you can avoid costly support workarounds.


## Responsibility for Quality - Dev vs. QA

According to Joel developers *race against the finish line*. Finish line means the code runs for the first time. "But try to break things? ... Not so much".

Testers have a different mindset and deliver tremendous input to the project.

I am sure I missed out lots of stuff but I hope the information I recollect from the event still makes sense and proves helpful to you.


Best,
Mark


## Resources

* [Things You Should Never Do](http://www.joelonsoftware.com/articles/fog0000000069.html)
* [S-O-L-I-D](https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)
* [Dr. Geoffrey Moore](https://en.wikipedia.org/wiki/Geoffrey_Moore#Core_and_context)
* [More Joel on Software book](https://www.amazon.com/More-Joel-Software-Occasionally-Developers/dp/1430209879/)
