---
layout: page
title: pH Sensors In Elsinore
tagline: "For all your basic needs!"
description: ""
categories: Elsinore strangebrew beer controller pH sensor acid base alkali
---
{% include JB/setup %}

pH Sensors Now Supported By Elsinore!
===============

Thanks to cank on HBT who purchased me a [DF Robots SEN0161](http://dfrobot.com/wiki/index.php/PH_meter%28SKU:_SEN0161%29) pH Sensor (because he purchased one too), I have added support for pH Sensors.

pH Sensors are easy for me to expand (I just need to write a single function for each one that's available

Hardware
==========

I have the dF Robots SEN0161 as a reference pH Sensor. You shouldn't leave a pH probe in a dirty solution (i.e. the mash or the boil or anything) since it degrades the sensor. When you want to take a reading, ensure the sample is in the safe range of your pH Probe in terms in temperature.

I strongly recommend using a [DS2450 expansion board](http://pcsensor.com/index.php?_a=product&product_id=43) to provide four analog inputs. I replaced the jack on the end with an XLR jack since all my temperature probes use XLR jacks. You'll need to validate which wire is the 5V, GND, and Data since I'm not 100% certain on the wiring colors being consistent.

And that's it... rather simple. Though I would recommend picking up some reference solutions to allow you to calibrate the sensor every now and again.

Setup
==========

In Edit mode, you will see a pH Sensor section appear. Clicking the ``` Add pH Sensor ``` button will show a popover that lets you add a pH sensor.

![New pH Sensor](http://i.imgur.com/8JaeFou.png)

You can set the name, the analog pin, choose the DS2450 address and set the offset. You can also use this to calibrate. For example, if you've got the probe in a known 7.0 pH solution, you can enter 7.0 in the box and an offset will be applied. For the SEN0161, the tolerance is 0.3 so unless the reading is over 0.3 out, no offset will be set.

![pH Sensor Setup](http://i.imgur.com/i2T5DsB.png)

Pressing the ``` Update ``` button will save the pH Sensor.


Usage
============

The pH sensor you've created will have a ``` Update Value ``` button

![Update Value](http://i.imgur.com/BMKbHju.png)

When pressed the pH value will be read and the pH value will be displayed in the button. You can press it again to update.

![Updated Value](http://i.imgur.com/1hClXkm.png)

This is my reading of a 4.0pH Solution
