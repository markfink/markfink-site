---
layout: post
title: CMock
subtitle: unit testing ESP-32 code
bigimg: /img/susan-mohr-572895-unsplash.png
tags: [microcontroller, cloud, iot, esp32, test automation]
---

Today I will let you in on a secret... on how to test embedded C programs. The unit testing framework [Unity](https://github.com/ThrowTheSwitch/Unity) is already part of [ESP-IDF](https://github.com/espressif/esp-idf) and is pretty straight forward to use.

But we embedded software developers usually need to deal with hardware dependencies. Hardware dependencies? We typically see one of the following:

* skip unit testing altogether - it is just too damn hard (but not for me and you...)
* use a mock framework

We use mocks to replace hardware dependencies with code. Often the hardware is not ready or we want to test on an environment where is not available (like for example continuous integration).

To mock out hardware dependency makes writing unit-tests much easier. We focus on testing the code of our embedded application using the interface of the hardware dependency.

Sure, we need to test our code with the real hardware dependency. But this is not unit-testing - this is integration-testing.

Enough said, lets look into some code!

The simplest embedded code sample **cmp_demo.c**:

{% highlight C %}
#include "dep_demo.h"
#include "cmp_demo.h"

int cmp_init(void) {
    int value = 42;
    return dep_init(value);
};
{% endhighlight %}

The interface of the hardware dependency **dep_demo.h**:

{% highlight C %}
#ifndef DEP_DEMO_H
#define DEP_DEMO_H

int dep_init(int);

#endif /* DEP_DEMO_H */
{% endhighlight %}


And the unit test **test_cmp_demo.c**:

{% highlight C %}
#include "unity.h"
#include "cmp_demo.h"

#include "mocks/mock_dep_demo.h"

TEST_CASE("test cmp_demo init", "[demo]")
{
    dep_init_ExpectAndReturn(42, 420);

    TEST_ASSERT_EQUAL_INT(420, cmp_init());
}
{% endhighlight %}

Our test includes **mocks/mock_dep_demo.h** and we tell it how the mock should behave "dep_init_ExpectAndReturn(42, 420);".

To make this work all we need to do is to tell the build system to create the mock based on the interface. Just add this to **CMakeLists.txt**:

{% highlight CMake %}
set(COMPONENT_SRCS "test_cmp_demo.c")
set(COMPONENT_ADD_INCLUDEDIRS "." "../include")

set(COMPONENT_REQUIRES unity cmock cmp_demo)

register_component()

#  CREATING THE MOCK  #
get_filename_component(header_abs_path ../include/dep_demo.h REALPATH )
create_mock(mock_dep_demo ${header_abs_path})
{% endhighlight %}

I left out some details for brevity. [Here you can find the complete sample code including CMock.](https://github.com/finklabs/esp32/tree/master/cmock_demo)

I opened a [ticket with Espressif](https://github.com/espressif/esp-idf/issues/2900) and I hope that they will include CMock in the standard ESP-IDF release.

I hope this post is helpful to you.

All the best, Mark

## Resources

* [Test Driven Development for Embedded C](https://www.amazon.com/Driven-Development-Embedded-Pragmatic-Programmers/dp/193435662X/)
* [ThrowTheSwitch](http://www.throwtheswitch.org/)
* [Unity](https://github.com/ThrowTheSwitch/Unity)
* [CMock](https://github.com/ThrowTheSwitch/CMock)
* [Complete CMock sample code](https://github.com/finklabs/esp32/tree/master/cmock_demo)
