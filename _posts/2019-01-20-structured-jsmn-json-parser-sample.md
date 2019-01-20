---
layout: post
title: C Json parser
subtitle: structured code
bigimg: /img/ryoji-iwata-669950-unsplash.png
tags: [microcontroller, esp32]
---

I recently had to **parse Json data** on a small embedded system. When looking for tools to help with this, I found and loved Serge Zaitsev's **jsmn** (pronounced "Jasmine").

Jsmn is written in C and considered one if not the most efficient Json parser in the field. Its philosophy is to be as simple as possible: no dynamic memory allocation, no callbacks, and absolutely no dependences. It's a great piece of software, but it is a bit light on examples especially for parsing bigger json data structures. I got stuck and asked a [question on how others do structure their parsers](https://github.com/zserge/jsmn/issues/150) but so far nobody shared a working solution.

I needed to split the Json parser into multiple functions. Mostly because I do not like big junks of code and I need to be able to unit-test smaller pieces of my code like the specialized parser functions.

Some sample Json data to parse:

{% highlight txt %}
  {
    "sense": [
      {
        "name": "inside",
        "component": "bme280"
      },
      {
        "name": "outside",
        "component": "bme280",
        "params": ["119", "120"]
      }
    ],
    "user": "mark",
    "unex": "pected"
  }
{% endhighlight %}


I studied all jsmn samples on the web I could find but did not find a simple solution I liked so I had to come up with something myself. The solution I came up with is really, really simple - in the past this almost always proved to be a reliable indicator for a good solution. So I wrote this post to share it with you.

First I parse the Json data into an **array of tokens**:

{% highlight txt %}
int i = 0;
int r;
jsmn_parser p;
jsmntok_t tokens[128]; /* We expect no more than 128 tokens */

// parsed the string into tokens using jsmn
jsmn_init(&p);
r = jsmn_parse(&p, JSON_STRING, strlen(JSON_STRING), tokens, sizeof(tokens)/sizeof(tokens[0]));
if (r < 0)
{
  printf("Failed to parse JSON: %d\n", r);
  return EXIT_FAILURE;
}
{% endhighlight %}

Now I process the array with specialized parser functions like here:

{% highlight txt %}
parse_sense_object(&i, tokens);
parse_actor_object(&i, tokens);
{% endhighlight %}

Each parser function advances the **index i** into the **tokens array**. Since C has no pass-by-reference I need to hand in a pointer to i.

The test case prints out a lot of information so it is easy to see what is going on from the output of running the test case on esp32:

{% highlight txt %}
...
Running jsmn demo split parser into smaller parts test...
root_size: 21
- Sense:
  size: 2
  o Instance:
    size: 2
    i: 4; k: 0
    Name: inside
    i: 6; k: 1
    Component: bme280
  o Instance:
    size: 3
    i: 9; k: 0
    Name: outside
    i: 11; k: 1
    Component: bme280
    i: 13; k: 2
    Params:
    size: 2
    * 119
    * 120
Unexpected key: unex
Unexpected key: pected
/home/mark/devel/10_esp32/esp32/jsmn_demo/test/main/test_app.c:159:jsmn demo split parser into smaller parts test:PASS
{% endhighlight %}

I commited the [complete sample code to my github](https://github.com/finklabs/esp32/blob/master/jsmn_demo/test/main/test_app.c) - feel free to take a look.


I hope this post is helpful to you.

All the best, Mark


## Resources

* [jsmn](https://github.com/zserge/jsmn)
* [comparison and microbenchmark of C Json parsers](https://translate.google.com/translate?hl=en&sl=ru&u=https://lionet.livejournal.com/118853.html)
