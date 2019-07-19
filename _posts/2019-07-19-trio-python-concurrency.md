---
layout: post
title: Trio – a friendly Python library
subtitle: for async concurrency and I/O
bigimg: /img/rob-wingate-nQYqEwimp5o-unsplash.png
tags: [python, software engineering]
---

Our world is inherently parallel and I am convinced that our programming languages must provide adequate abstractions so we can model our world while keeping our sanity. Python always had many tools, frameworks and techniques for implementing concurrent behaviour. But there was never an obvious way to do things (I wrote about [Python concurrency](https://www.mark-fink.de/2016-06-12-please-remove-the-gil/) earlier).

In 2016 I learned Golang because of its superior concurrency mechanisms. I like Golang and there is nothing wrong with it but I still do most of my work in Python. So this solution did not really work out for me.

Python2 will not be maintained after 2019. This marks a major milestone for the Python community and we will celebrate the happy lifecycle completion of this great technology. Looking forward many of us can now drop Python2 compatibility which opens up access to new Python3 features. In this spirit I looked at Python concurrency again...

I found this great Pycon talk by Nathaniel J. Smith (I particularly liked the 50+ year history outline on the problem):

[![Trio: Async concurrency - PyCon 2018](https://img.youtube.com/vi/oLkfnc_UMcE/0.jpg)](https://www.youtube.com/watch?v=oLkfnc_UMcE)

I looked into Trio and I must say I am impressed. The documentation is well written and Trio provides us with useful tools to implement concurrent behaviour in Python. They even thought about test utilities that help writing pytests for our concurrent solutions.

When growing a Python codebase for some time it kind of degrades. A coworker called this bit-rot and I believe this is really what happens ;). When working with real world application we constantly have to deal with latencies. And there are quick workarounds. We add a time.sleep() here or poll for an event there. If you think I am on to something then just grep for "time.sleep" in your codebase and you get the number of potential issues you probably need to be dealing with soon.

Trio provides us with useful abstractions that lead to readable code. The following shows a sample on how to properly implement a timeout using Trio:

{% highlight python %}
import trio

TIMEOUT = 1

async def do_sth():
    with trio.move_on_after(TIMEOUT) as scope:
        a = 0
        while 1:
            await trio.sleep(0)  # necessary checkpoint!
            a += 1
        print('done: %d' % a)

    if scope.cancelled_caught:
        # cleanup could be done here or in except trio.Cancelled block
        return False
    return True


def main():
    run_to_completion = trio.run(do_sth)
    print('completed task: %s' % run_to_completion)


if __name__ == '__main__':
    main()
{% endhighlight %}


Don't worry I am not going through the whole [core functionality for Trio](https://trio.readthedocs.io/en/latest/reference-core.html#). There is much more including interactions with threads from 3rd party libraries. I just want to demo the **Nursery** feature. I am convinced that this is a great way to simplify writing concurrent solutions.


{% highlight python %}
import trio


async def compute(start, end, res):
    res.append(sum(range(start, end)))


async def compute_all():
    results = []
    async with trio.open_nursery() as nursery:
        nursery.start_soon(compute, 0, 100, results)
        nursery.start_soon(compute, 100, 200, results)

    return results


def main():
    res = trio.run(compute_all)
    print('sum: %d' % sum(res))


if __name__ == '__main__':
    main()
{% endhighlight %}


Trio provides a context manager **open_nursery()** which enables you to keep control over the concurrent executions. This allows you to deal with exceptions in concurrent code so you end up with correct solutions where you need concurrency.

I can't say whether Trio solves all our problems - probably not - but I am convinced that it is a big step in the right direction for us.

Best,
Mark

## Resources
* [Python2 EOL](https://pythonclock.org/)
* [Trio](https://trio.readthedocs.io/en/latest/)
* [Nursery](https://vorpus.org/blog/notes-on-structured-concurrency-or-go-statement-considered-harmful/)
* [PyCon 2018 talk on async concurrency](https://vorpus.org/blog/companion-post-for-my-pycon-2018-talk-on-async-concurrency-using-trio/)
