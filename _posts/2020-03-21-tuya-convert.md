---
layout: post
title: Ending the IoT cloud bundling battle
subtitle: how Open Source stops your light bulbs from calling home
bigimg: /img/damir-spanic-lb7q0iLOaSE-unsplash.png
tags: [iot, microcontroller]
---

I am a Linux user by heart. So I enjoy my freedom to decide when and if it is time to do upgrades or buy new hardware. And I totally hate it when a company decides after 15 month that I can't get any updates for my perfectly fine TV or Android tablet.

Reliability is also a big concern here. My internet is down only about once or twice a year and I understand that the telco provider cant do much about an excavator pulling out the glasfaser. But I still want to be able to use my lights and doors during such an event. Someone else running over-the-air updates on devices connected to my network is out of the question for me.

The [Tuya-Convert](https://github.com/ct-Open-Source/tuya-convert) project is great since it allows us to free our smart devices from their default cloud connection.

Tuya-Convert consists of multiple parts. You need a Raspberry-Pi to act as a Wifi access point and a donor-device (wemos d1 mini or similar/ your mobile phone). This whole setup tricks the smart device into accepting an over-the-air (OTA) update with your desired firmware. Currently most smart devices (>11.000 products) are based on Tuya TYWE3S (a miniature ESP8266 board) - the scope of Tuya-Convert is currently limited to this environment. So if you plan to go shopping for IoT devices make sure they are based on TYWE3S!

If you are curious for more details (35CC presentation - auf deutsch, an english translation is available, too):

[![Presentation 35CC (deutsch)](https://img.youtube.com/vi/urnNfS6tWAY/0.jpg)](https://www.youtube.com/watch?v=urnNfS6tWAY)

The firmware used to upload to the devices usually is tasmota but you totally are able to bake and use your own firmware. Tasmota comes with all you usually need (documentation, community, forum, ...) and makes it easy to integrate the smart device with an MQTT server (like for example ioBroker).

The whole situation totally reminds me of the painful browser wars that escalated into the U.S. antitrust courts stopping Micro$oft from locking out other browser vendors from the operating system they sold. This situation took forever to resolve and caused a lot of pain for users, browser vendors and developers. I hope that at least some of the IoT device manufacturers are way more clever than Micro$oft was at the time.

Thanks to the Tuya-Convert and Tasmota developers I am looking forward to great times using my liberated IoT devices.


Best,
Mark


## Resources
* [Escaping the IoT-Cloud](https://www.heise.de/ct/artikel/Tuya-Convert-Escaping-the-IoT-Cloud-no-solder-needed-4284830.html)
* [Tasmota Firmware](https://github.com/arendst/Tasmota)
* [ioBroker home automation](https://www.iobroker.net/)
* [Antitrust law case U.S. government vs. Microsoft](https://en.wikipedia.org/wiki/United_States_v._Microsoft_Corp.)
