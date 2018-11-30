---
layout: post
title: Hard to test code
subtitle: 
bigimg: /img/frank-vex-1123999-unsplash.png
tags: [software engineering, test automation]
---

I am not evangelizing TDD for various reasons but I would like to share an relevant observation which I frequently made while working on consulting projects. If developers do not know how to write tests or need to take shortcuts (in form of not writing tests) they usually end up with a codebase that is hard-to-test. I was recently asked to add tests to such a codebase. The project had a few tiny testcases. I quickly discovered that I can not write tests for the project without making the codebase testable first. Now I have to take the risk of refactoring without the safety-net of powerful tests.

Disclaimer: I am convinced that SOLID is harmful so if you are looking for something related you might get a little bit offended.

Sometimes existing code is hard to test. This means the code is not designed, organized and structured in a way that makes it testable. In my experience people who write testable code follow some guiding-principles. Usually these developers learned in their past projects how much they benefit from tests and learned how to write testable code. Misko Hevery gives a nice summary to this when he boldly observes "Well there are no tricks to writing tests, there are only tricks to writing testable code".

In my experience there are some common obstacles independent of programming language and test-tools. In this article I want to outline the most common ones and attempt to formulate guiding-principles on how to avoid them.


## API related problems

A common problem with code that has grown over time is that it is unclear what the API is. For example private methods often have a public signature or public methods lack documentation. In this case it is not clear what is called from outside code and who is dependent on this. 

A good practice would be to frequently revisit the API of your codebase. Make explicit what the API of your codebase is and provide documentation. Private methods should be kept private. With that you are able to restructure your code without breaking somebody else's code.

If parts of your API becomes obsolete than remove or deprecate it.


## Dependencies

Many problems with hard-to-test code originate from dependencies:

* Mixing new operator with application logic.
* Not using dependency injection (hard coded dependencies).
* Mixing application logic with configuration.
* Hard dependencies to supposedly plugable-code.

Dependency problems make it also difficult to reuse code. Over the last few years many developers became aware of this and today many project use technologies to manage configuration and to inject dependencies.


## Testability

Some issues have a direct relation with testability:

* Global state makes testing hard since tests change the state and it is difficult to keep track and clean up after test run.
* Singletons (global state in sheeps closing).
* OO: doing work in the constructor. This makes testing very hard. You need to expose the functionality and make it testable.

Avoid these problems and design your code for testability!


## Side Effects

For some application domains it is difficult to avoid side effects. This is the case especially if you work in polyglot environments with different technologies, protocols, etc. For example if you use a library that provides a programming interface to a service like boto3 / AWS.

But still you can try to avoid additional side effects:

* Calling exit in library code. Only the caller should exit - never exit in library code.
* Setting global state (see testability).


I hope this information is helpful to you.

All the best,
Mark


## Resources

* [top-10 things which make your code hard to test](http://misko.hevery.com/2008/07/30/top-10-things-which-make-your-code-hard-to-test/)
