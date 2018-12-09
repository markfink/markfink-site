---
layout: post
title: Alexa...
subtitle: turn on the light
bigimg: /img/johannes-plenio-262511-unsplash.png
tags: [iot, python, amazon aws, raspberrypi]
---

This week I bought an echo dot device and I wanted to try out some of its home automation features. I used [Home Assistant](https://home-assistant.io) (Python, Open Source).

For my test setup I added a LED on RPI port 18 (I used a 68 ohm resistor).

[![Alexa test setup](https://img.youtube.com/vi/gFoLOIzLByU/0.jpg)](https://www.youtube.com/watch?v=gFoLOIzLByU)


## Install Home Assistant on Raspberry Pi

I followed the [documentation](https://home-assistant.io/getting-started/installation-raspberry-pi/#manual-installation) for Home Asssistant for installation on a Raspberry Pi.

For headless setup, SSH can be enabled by placing a file named 'ssh', without any extension, onto the boot partition of the SD card.

{% highlight bash %}
$ ssh pi@raspberrypi
{% endhighlight %}

The default password of the RPI is raspberry. It is best to change the default password:

{% highlight bash %}
$ passwd
{% endhighlight %}


## Home Assistant configuration

The Home Assistant is configured via the yaml config-file configuration.yaml.

{% highlight bash %}
$ sudo su -s /bin/bash homeassistant
$ nano /home/homeassistant/.homeassistant/configuration.yaml
{% endhighlight %}

At the end of the configuration.yaml file I added the folowing lines to enable the GPIO pin 18 and expose it via emulated_hue:

{% highlight yaml %}
...
######## Changes by Mark ########
switch:
  platform: rpi_gpio
  ports:
    18: light

emulated_hue:
  type: alexa
  expose_by_default: true
{% endhighlight %}

Start Home Assistant service on the RPI:

{% highlight bash %}
$ cd /srv/homeassistant
$ . ./homeassistant_venv/bin/activate
$ hass
{% endhighlight %}


## GPIO Switch setup

I am using Home Assistant's [rpi_gpio switch platform](https://home-assistant.io/components/switch.rpi_gpio/) to control the LED via the RPI's GPIO pin.

For this to work I had to add the homeassistant user to the gpio group:

{% highlight bash %}
$ sudo adduser homeassistant gpio
{% endhighlight %}

[For detailed RPI pin info](https://en.wikipedia.org/wiki/Raspberry_Pi#GPIO_connector)


## Alexa discover devices

For the device discovery part I asked alexa to do the work:

{% highlight bash %}
!! alexa, discover devices
{% endhighlight %}

Visit [Alexa Setup](http://alexa.amazon.de/) to setup a "desk" group which contains the light device:

![Alexa setup device details](/media/alexa_lights/alexa_devices.png){: width=600}

![Alexa setup desk device group](/media/alexa_lights/alexa_desk_group.png){: width=600}


## Using Alexa

Now I can use Alexa to switch the light on and off...

{% highlight bash %}
!! alexa, turn desk light on
!! alexa, turn desk light off
{% endhighlight %}


I wish you a happy new year!
Mark


## Resources

* [https://home-assistant.io](https://home-assistant.io)
* [https://www.youtube.com/watch?v=Cfasc9EgbMU](https://www.youtube.com/watch?v=Cfasc9EgbMU)
* [https://www.amazon.com/echo-dot](https://www.amazon.com/echo-dot])
