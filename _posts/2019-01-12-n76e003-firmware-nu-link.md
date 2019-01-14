---
layout: post
title: Nuvoton N76
subtitle: flash firmware using Linux
bigimg: /img/arthur-aldyrkhanov-566881-unsplash.png
tags: [microcontroller, n76]
---

If you know anything about microcontrollers you most likely know that **blinking a LED** on the microcontroller development board is what we call a **hello-world** program for other technologies. Over the years I have done this exercise 10 times or more using different microcontrollers and boards. Once the board-specifics, compiler configurations, flashing firmware are all figured out, one can take a faster pace but without this first steps one can not do anything with the microcontroller at all. And for sure each microcontroller offers its unique challenges. Today I have spent the better part of the day figuring out **how to get started with the N76 on Linux**.

![blink N76](/media/n76_numicro_flash/n76e003_linux_upload_firmware.gif)

I have an interest in [Value Line Gadgets](https://github.com/TG9541/stm8ef/wiki/STM8S-Value-Line-Gadgets) like the ones mass produced in China. Till about fall 2018 many of these have been equipped with STM8 chips or equivalents. Today if you order such a component it is a pretty safe bet that the **STM8 has been replaced by the pin compatible Nuvoton N76E003AT20**. Many argue that this has to do with costs per unit but I can not say for sure. Few weeks ago I found a fantastic site [THE AMAZING $1 MICROCONTROLLER](https://jaycarlson.net/microcontrollers/). Jay Carlson goes into all details on 21 different microcontrollers in that segment including pros, cons, tooling, etc. To me it was the most impressive work I have seen in all 2018 by far! Of course he covers the [Nuvoton N76](https://jaycarlson.net/pf/nuvoton-n76/).

Big chip manufacturers often provide proprietary IDEs, frameworks and such but in the case of cheap mass market chips they often go with Keil or IAR. I can not say anything against these tools but they are Windows only and I am in favour of Linux and Open Source tools. We have the **small device C compiler SDCC** that supports the **8051 architecture** of the N76. Nuvoton offers the NuMicro ICP software for uploading the firmware. The NuMicro is also a Windows tool but it almost works on Linux using wine. Compared to the STM8 the Linux & Open Source tooling is far from optimal but I stay positive and look forward to better Linux support in the future.

Enough said, lets look into microcontroller hardware! I use the Nuvoton NuLink programmer (red component in the photo above) and a N76E003 development board (blue component).

One of the challenges I faced today with this new board was that unlike other development boards the one for N76 has the onboard LED connected via **jumper J2**. J2 is missing in this version and I had to solder in a bridge for J2 before the onboard LED could be used.

The nu-link programmer is connected to the laptop via USB. For it to work on Arch Linux I had to add the "/etc/udev/rules.d/88-nulink.rules" file with config:

{% highlight txt %}
ATTRS{idProduct}=="511b", ATTRS{idVendor}=="0416", MODE="0666", GROUP="plugdev"
ATTRS{idProduct}=="511c", ATTRS{idVendor}=="0416", MODE="0666", GROUP="plugdev"
ATTRS{idProduct}=="511d", ATTRS{idVendor}=="0416", MODE="0666", GROUP="plugdev"
ATTRS{idProduct}=="5200", ATTRS{idVendor}=="0416", MODE="0666", GROUP="plugdev"
{% endhighlight %}


Now, lets look into some code!

Here the simple blink sample **gpio.c**:

{% highlight C %}
#include "N76E003.h"
#include "SFR_Macro.h"
#include "Function_define.h"
#include "Common.h"
#include "Delay.h"

void setup(void);

void main(void)
{	
	setup();
	
	while(1)
	{
		if(P05 != 0x00)
		{
			Timer0_Delay1ms(900);
		}
		
		set_P15;
		Timer0_Delay1ms(300);
		clr_P15;
		Timer0_Delay1ms(300);
		set_P15;
		Timer0_Delay1ms(300);
		clr_P15;
		Timer0_Delay1ms(1000);
	};
}

void setup(void)
{	
	P15_PushPull_Mode;
	P05_Input_Mode;
}
{% endhighlight %}


The rest of the code is my quick & dirty port of Nuvoton's sample for Keil. So far I ported only the parts I needed for this blink sample. [Here you can find this hack including Makefile](https://github.com/finklabs/n76/tree/master/blink_first_draft).

![Using the NuMicro software to flash the firmware](/media/n76_numicro_flash/numicro_falsh_N76E003.png)

Running **NuMicro on Linux using wine** overall is at best a strange experience. The software can not be used without mouse so no-way for automation! And the mouse does only work 30% of the time. If the mouse is not working I have to close NuMicro and restart it. If the mouse is working then flashing the firmware works reliable.

Like I said before I **hope for better Linux tooling** to support flashing the N76 from the command line. Something as good as for example [stm8flash](https://github.com/vdudouyt/stm8flash) for the STM8s. Till then I hope somebody comes up with a better way of using the NuMicro on Linux by fine tuning wine or using Docker...

Don't get me wrong if I was using the N76 professionally, I would follow Jay's suggestion to buy a Windows laptop and a Keil license. For writing some small programs in my spare time this will do for now.


I hope this post is helpful to you.

All the best, Mark

## Resources

* [STM8S003](https://www.st.com/content/ccc/resource/technical/document/datasheet/42/5a/27/87/ac/5a/44/88/DM00024550.pdf/files/DM00024550.pdf/jcr:content/translations/en.DM00024550.pdf)
* [THE AMAZING $1 MICROCONTROLLER](https://jaycarlson.net/microcontrollers/)
* [Nuvoton N76E003AT20](https://www.nuvoton.com/hq/products/microcontrollers/8bit-8051-mcus/low-pin-count-8051-series/n76e003/?__locale=en)
* [Keil](https://www.keil.com/download/product/)
* [SDCC Compiler](http://sdcc.sourceforge.net/)
