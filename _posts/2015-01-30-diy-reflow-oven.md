---
layout: post
title: DIY Reflow Oven
subtitle: get your own PCB production going!
bigimg: /img/nicolas-thomas-533958-unsplash.png
tags: [arduino, microcontroller]
---

One of my new years resolutions was to turn a pizza oven into a SMT reflow oven. Awkward...

Yet here I am. For my microcontroller projects I like to manufacture my own PCB boards and a industry-grade reflow oven is just too expensive. Administering the reflow process manually is to cumbersome and not really an option. The following diagram shows a typical reflow temperature profile. Any significant deviation from this profile might ruin your board assembly.

![a typical reflow temperature profile](/media/diy_reflow_oven/reflow_profile.png){: width=600}

Many makers mastered this situation before and the solution in many cases is a DIY reflow oven like the one I am introducing here.

![opening up the pizza oven](/media/diy_reflow_oven/opening.png){: width=600}

I kept the original dial, clock and safety mechanisms of the oven intact. I just added the solid state relay (ssr) in line so the Arduino controller can switch the oven off when it is getting too hot. In this way the temperature in the oven follows exactly the desired reflow profile. A k-type thermocouple is used to measure the temperature inside of the oven close to the PCB board.

![adding a solid state relay](/media/diy_reflow_oven/adding_ssr.png){: width=600}

![testing the components](/media/diy_reflow_oven/test_drive.png){: width=600}

I mounted the ssr with its metal cooler to the bottom of the oven so it uses the cool air that comes in through the oven air holes.

During test drive I realized that the micro-controller software that came with the Arduino reflow shield has some problems and does not exactly behave as I expected. In my opinion a PID controller in this case makes things overly complicated so I wrote my own controller software which is way simpler and follows exactly the configurable temperature profile (see resources section).

I decided to mount the Arduino including reflow shield on top of the oven (as you can see in the photo below). In this way the controller stays cool and I have easy access to buttons and USB in case I need to flash the controller.

![reflow oven assembled](/media/diy_reflow_oven/assembled.png){: width=600}

If you use a different reflow paste you might have to adjust the following parameters:

{% highlight C %}
	#define RAMPUP 3.0
	#define SOAK_TEMPERATURE 150
	#define SOAK_PERIOD 90000
	#define PEAK_TEMPERATURE 237
	#define PEAK_PERIOD 50000
{% endhighlight %}

The complete reflow-cycle takes about 15 minutes and the controller beeps once the process is completed.

Best,
Mark


## Resources

* [Reflow soldering](http://en.wikipedia.org/wiki/Reflow_soldering)
* [Surface Mount Technology](http://www.amazon.com/Mastering-Surface-Mount-Technology-LabworX/dp/1907920129/)
* [arduino controller shield](http://www.rocketscream.com/blog/product/reflow-oven-controller-shield-arduino-compatible/)
* [Solid state relay](http://en.wikipedia.org/wiki/Solid-state_relay)
* [thermocouple](https://learn.adafruit.com/downloads/pdf/thermocouple.pdf)
* [my code](https://github.com/markfink/ReflowOvenController.git)
