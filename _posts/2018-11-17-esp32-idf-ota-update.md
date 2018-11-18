---
layout: post
title: ESP-32 over-the-air (OTA) update
subtitle: with some bits on partitions
bigimg: /img/alain-pham-248578-unsplash.png
tags: [microcontroller, cloud, iot, esp32]
---

Flashing microcontroller firmware is easy especially if you use ESP-IDF. And this is almost always true as long as you are using a development board with USB connector and the device sits around on your desk. For IoT devices you want over-the-air (OTA) updates. Instead of retrieving the device for update or even visiting it on-site you upload the new firmware to the cloud and send a message to the device with the update request. We are all pretty familiar with the ota update process from using smart phones.

For oto updates we need to prepare two app partitions on the device. But first we need to cover some basics...


# Partition Table

I do not cover ESP-32 partitions in all depth here. Lets just say that partitions on ESP-32 are used in similar ways like the storage medium on your laptop is organized. ESP-IDF comes with meaningful defaults "Single factory app, no OTA" which is suitable for experiment projects. If you want to use OTA updates then what you probably need is "Factory app, two OTA definitions". So after downloading the firmware update it is stored on the alternate app partition that is used for the subsequent boot. I should mention that there is also an "expert mode" called "Custom partition table CSV" where you can specify the partitions using a CSV file. There is also ample of tool support to build the "expert mode" partitions and work with the data.

For the OTA updates I use the "Factory app, two OTA definitions" mode which I set using "make menuconfig":

![Screenshot set 2 OTA partitions](/media/esp_ota_update/screenshot-partition-table.png)


I should also mention that with the available default partition settings in "make menuconfig" there is also a NVS (none volatile storage) partition put in place on the device. The NVS partition is intended to be used as a key-value store for data that you want to survive a reset or even an OTA update.

This is as far as I go concerning partitions. There is a wealth of features waiting for being discovered like for example encrypted partitions etc. Please consult the excellent documentation.


# Many degrees of freedom to download the firmware

Naturally there exists a multitude of ways to provide the firmware binaries to update your esp32 project (even if you are focused on AWS). I did quite a bit of research and I like this variant best:

* create a Amazon *S3 bucket* to store your firmware releases
* upload the firmware binary to the S3 bucket
* create a *presigned url* (has expiry date, default is 3600 sec.)
* publish the presigned url on the devices MQTT *update topic*

    
# Building and uploading the firmware

Using ESP-IDF for building your firmware binaries is quite simple:

{% highlight bash %}
$ make
{% endhighlight %}


You find the firmware binary in "build/<your_project>.bin". The binary for OTA update is the same as for "factory app" (quite exiting). So the difference in using OTA updates is in the *partition table* and not the binary.

Then upload the firmware binary to your Amazon S3 bucket.


# Create a presigned URL for firmware download:

{% highlight bash %}
$ aws --endpoint-url=https://s3.eu-central-1.amazonaws.com s3 presign s3://farm-iot-bin/hello-world.bin --expires-in 600

https://s3.eu-central-1.amazonaws.com/farm-iot-bin/hello-world.bin?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAJG6N4L4QAVOPYXBQ%2F20181101%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Date=20181101T151513Z&X-Amz-Expires=600&X-Amz-SignedHeaders=host&X-Amz-Signature=8abf23dfb2352febf71c5813862be440d7f6acd53aa1f901543b70d23bea9cc5
{% endhighlight %}

Note the 600 means 10 minutes and you can not use the url to download the firmware after the presigned url has expired.

Add the url to a message (just fill in the "update_url" attribute {'update_url': 'https://...'}):

![Requesting the device to update](/media/esp_ota_update/screenshot-ota-update-request.png)



# OTA update code

Your project code needs to implement the OTA update capability... Setting the partition table is just the preparation.

My "iot-bme280" projects has OTA update capability:

![Requesting the device to update](/media/esp_ota_update/code-esp-https-ota.png)

(the complete iot-bme280 project code you can find ['here'](https://github.com/finklabs/esp32.git))


# Erasing the NVS

Sometimes it is necessary to erase the NVS flash storage, the build system comes with the right tool for that, too:


{% highlight bash %}
$ make erase_flash
{% endhighlight %}


# Example blink demo

I did not prepare a *dedicated* example for the OTA update. You can have a look at the [system/ota](https://github.com/espressif/esp-idf/tree/master/examples/system/ota) examples that come with ESP-IDF. I found the README.md quite helpful.

Besides all of that I just used the *blink_demo* firmware binary to experiment with and demo OTA-updates.


I hope this post is helpful to you.

All the best, Mark


## Resources

* [ESP-32](https://www.espressif.com/en/products/hardware/esp32/overview) - successor to ESP-8266
* [Partition Tables](https://docs.espressif.com/projects/esp-idf/en/latest/api-guides/partition-tables.html)
* [ESP-IDF ota updates](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/system/ota.html)
* [Custom partition table CSV](https://medium.com/the-esp-journal/building-products-creating-unique-factory-data-images-3f642832a7a3)
