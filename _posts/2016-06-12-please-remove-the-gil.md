---
layout: post
title: Concurrent Python
subtitle: please remove the gil
bigimg: /img/nick-fewings-jCHWT477xB4-unsplash.png
tags: [python]
---

I have recently watched Larry Hastings talk about *Removing Python's GIL: The Gilectomy* that has been recorded at *PyCon 2016*. Larry very graphically outlines the problems from not having proper concurrency features. He also tells a nice story on how the Python community is struggling with this situation for the last 24 years.

[![Great talk summarizing the Python GIL problem](https://img.youtube.com/vi/P3AyI_u66Bw/0.jpg)](https://www.youtube.com/watch?v=P3AyI_u66Bw)

Regarding **concurrent Python** I researched options like twisted, stackless, multiprocessing, etc. quite a while ago. I finally had to give up and move on. I still use Python, but for solutions that require proper concurrency I use Golang. If you monitor closely the DevOps tool space you will probably notice that I am not alone with this view.

When I noticed the discussion about the Gilectomy some curiosity sparked within me and I watched the talk to get some idea about state of affairs. The talk gives a lot of background and detailed insights. The Gilectomy is an attempt to solve concurrency in Python in a generic way. Larry makes a clear case that Python is extremely optimized to run single threaded. Removing the GIL works but does not make sense from a performance perspective. Given the current Python memory allocation strategy my personal summary is that the Gilectomy is a hopeless case.

I recommend to approach this problem starting from a **proper programming model for concurrency**. In my opinion a must-have for maintainable concurrency code. Golang makes an excellent case to prove how this can and should be done. I am convinced that using this model for Python concurrency would dramatically simplify the implementation and addresses most of the performance problems of a generic solution. I am in the spectators seat with this so I probably won't be heard but I wrote an email to Larry Hastings anyway...


{% highlight txt %}
Hi Larry,

I have seen your talk yesterday and I must say I admire your enthusiasm.

Let me put a few things out of the way:
* I like Python a lot
* I always had a lot of concerns regarding not having proper concurrency mechanisms in Python
  for the very same reasons that you outline in your talk. I do not think that twisted and
  friends are proper ways to solve the issues.
* I am very happy with Golang since it has proper concurrency mechanisms. So if I need safe
  and simple concurrency I use Golang.
{% endhighlight %}

Besides having a solid and almost pythonic solution at hand (by using Golang), I would still like to see Python with proper concurrency tools. I am not a core developer but I understand the problems you describe in your talk. I believe adding specific language features is the way to go. Golang provides go-routines and channels for developers to tackle concurrency problems. I think by recreating these in Python you can both preserve execution speed, remove (limit) complexity and as a plus you add a proper model for concurrent programming. I guess my question is have you tried that and what do you think about it?

I did not get an answer from Larry so far... But anyways, I hope that the Python community is soon going to address the Python concurrency issues and that they will manage to overcome all obstacles. Please do not wait another 24 years to solve this!


update 13.06.2016 (PyPy does not have these restrictions, thanks Charlie for the heads-up):

[![Armin Rigo - The GIL is dead: PyPy-STM](https://img.youtube.com/vi/e8wUiGDDVno/0.jpg)](https://www.youtube.com/watch?v=e8wUiGDDVno)


Depending on your application PyPy might be a great solution that you should consider. As far as I can see there are mixed reports about PyPy support for NumPy, SciPy, Matplotlib, Pandas, Sklearn and friends. I will definitely keep an eye on PyPy myself. For now I make a promise that as soon as I see the first Pandas + Jupyter notebook running on PyPy I will try it out myself.

Another thing Charlie pointed out is Python 3.5 asyncio. Amongst other things it provides **asyncio.coroutines**. I could not find a comprehensive performance evaluation so I am not yet convinced that this is a great multicore solution. I put this on my todo list and I will let you know.

I hope you do not get the impression that I focus on the negative;) Just to make sure I like to recommend to you a talk by David Beazley. Somehow he manages to present the whole situation as an exiting adventure. You have to see this! It is incredible...

[![Python Concurrency From the Ground Up](https://img.youtube.com/vi/MCs5OvhV9S4/0.jpg)](https://www.youtube.com/watch?v=MCs5OvhV9S4)

Best,
Mark

## Resources
* [Great talk summarizing the Python GIL problem](https://www.youtube.com/watch?v=P3AyI_u66Bw)
* [Python multiplocessing docs](https://docs.python.org/2/library/multiprocessing.html)
* [StacklessPython](https://wiki.python.org/moin/StacklessPython)
* [Twisted](https://twistedmatrix.com/trac/)
* [Article on Golang](https://www.thoughtworks.com/radar/languages-and-frameworks/go-language)
* [PyPy](http://pypy.org/)
