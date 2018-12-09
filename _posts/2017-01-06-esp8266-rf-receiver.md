---
layout: post
title: Find codes used by RF radio control
subtitle: using ESP-8266
bigimg: /img/james-sutton-188689-unsplash.png
tags: [iot, home automation, arduino, microcontroller]
---

This week I bought a set of radio controlled power outlets. My plan is to use [Home Assistant](https://home-assistant.io) (Python, Open Source) to control the power outlets. For that to work I need to find the codes that are used by the remote control's 433 Mhz radio transmitter to switch the power ON and OFF (each power outlet has two codes).

First I connect the 433 Mhz receiver to my Wemos D1 (ESP8266). I use the Wemos since it is still installed on my experiment board (after I found out the codes I do not need this setup any more).

![RF receiver connected to Wemos D1](/media/wemos_rf_receiver/wemos_rf_receiver.png){: width=600}


## Arduino Sketch

I like to use the Arduino IDE to write/ upload ESP8266 firmware.

{% highlight c %}
/*
  Simple RF receiver based on
  
  https://github.com/sui77/rc-switch/
*/

#include "RCSwitch.h"

RCSwitch mySwitch = RCSwitch();

void setup() {
  Serial.begin(115200);
  mySwitch.enableReceive(13);  // Receiver on interrupt GPio 13 => that is pin D7 
  Serial.println("ESP8266 RF receiver scanning now...");
}

void loop() {
  if (mySwitch.available()) {
    
    int value = mySwitch.getReceivedValue();
    
    if (value == 0) {
      Serial.print("Unknown encoding");
    } else {
      Serial.print("Received ");
      Serial.print( mySwitch.getReceivedValue() );
      Serial.print(" / ");
      Serial.print( mySwitch.getReceivedBitlength() );
      Serial.print("bit ");
      Serial.print("Protocol: ");
      Serial.println( mySwitch.getReceivedProtocol() );
    }

    mySwitch.resetAvailable();
  }
}
{% endhighlight %}


## Reading the codes

Once the code is uploaded to the ESP8266 it writes to the serial interface with 115200 baud. I press the different buttons on the remote control and in the Serial Monitor I see the related codes.

{% highlight txt %}
ESP8266 RF receiver scanning now...
Received 1234567 / 24bit Protocol: 1
Received 1234568 / 24bit Protocol: 1
Received 1234568 / 24bit Protocol: 1
{% endhighlight %}


I filled a spreadsheet with all ON / OFF codes for all my 5 power outlets. With these codes I am prepared to connect more devices to Home Assistant.

![Power outlet and remote control](/media/wemos_rf_receiver/elekcity_radio_plug_sockets.png){: width=600}


I hope this article proves helpful to you...
Mark


## Resources

* [https://home-assistant.io](https://home-assistant.io)
* [rc-switch library](https://github.com/sui77/rc-switch)
* [Etekcity Radio Plug Sockets](https://www.amazon.de/gp/product/B016I3TZ58/)
* [433 Mhz Transmitter & Receiver](https://www.amazon.de/gp/product/B01H2D2RH6/)
