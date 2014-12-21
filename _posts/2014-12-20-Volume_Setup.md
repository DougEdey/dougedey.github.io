---
layout: page
title: Volume Measurement Setup
tagline: Based off OSC Sys documentation
description: ""
categories: elsinore analog volume strangebrew brewery mpx5010D DS2450
---
{% include JB/setup %}

Volume Measurement Setup Guide
==============================

This guide is based off the BrewTroller setup, all of the code was engineered by myself, I just used the research that was done in the forums and their documentation which now appears to be fully defunct. There's a [Wayback snapshot](https://web.archive.org/web/20140815170908/https://www.oscsys.com/projects/brewtroller/system-design/volume-measurement) but I'll duplicate the information here. And update all BrewTroller References to Elsinore.

Overview
==============

Elsinore can use any 0-5V DC analog device to represent the current volume of a vessel. A set of calibrations for the vessel must be recorded to map specific signal values to known volumes. There are at least three calibrations that must be created per vessel to enable Volume measurement, but you can add as many as you want. Elsinore will use the map to plot values between calibration points.

The most common method used for measuring volume with Elsinor is using pressure sensors. As the height of the liquid increases in a vessel the pressure increases in a corresponding way. Measurement for initial filling can be quite accurate but as temperature decreases volumes will drift as a result of a small vacuum created by the air in the pick up tube connected to the pressure sensor. BrewTroller users cleverly discovered that using a small air pump and feeding a constant stream of air into the pick up tube would eliminate this vacuum and result in accurate volume readings across temperature changes.

Bubbler Theory
==============

A small air pump is used to force air (at a very low flow rate) into the pressure sensing tube. This forces air to bubble steadily out the end of the pickup tube. The pump runs at all times during use. By ensuring that the tubing is always completely full of air, the pressure reading is always consistent - most importantly, it does not vary with temperature, which is a non-trivial issue in a sealed-tube arrangement.

By its very nature, this arrangement is also immune to minor air leaks, and can recover from a temporary disconnection of the air line tubing (accidental or otherwise) during use, either of which are catastrophic in a sealed-tube setup.

There is also no significant risk of moisture/steam reaching the pressure sensor itself, due to the constant stream of air purging the tube.

One caveat of this setup is that the continuous formation and release of bubbles at the end of the pickup tube does introduce a steady ripple in the pressure sensor reading. Appropriate averaging in Elsinore, and/or hardware filtering, can reduce this significantly.

Hardware
===========

If you have a pressure sensor/analog input device that is 1.7v output max, you can get away with using the onboard BeagleBone Black inputs. However, the MPX5010D is 5v output and will break the analog pins.

For this reason, I strongly recommend using a [DS2450 expansion board](http://pcsensor.com/index.php?_a=product&product_id=43) to provide four analog inputs. I replaced the jack on the end with an XLR jack since all my temperature probes use XLR jacks. You'll need to validate which wire is the 5V, GND, and Data since I'm not 100% certain on the wiring colors being consistent.

Note: An Elsinore User will be selling expansion boards for Elsinore in early 2015.

In addition to the pressure sensors, air line, and dip tube needed for the standard sealed-tube arrangement, this method requires the addition of tee fittings, air flow valves, and a pump.

![Layout](http://i.imgur.com/mZHaw5o.gif)

All of these additional parts are available in the aquarium sections of typical pet shops - it should cost less than $15 for parts sufficient for 1-4 sensors.
A "gang valve" allows one pump to supply many sensors, with an air adjustment valve for each. Even the smallest aquarium air pump should suffice for this application.

Setup
============

As with any pressure sensor arrangement, the dip tube end should be placed as deep in the vessel as possible (to cover the widest range) and must be fixed in place, as any movement can throw off the reading.

Air flow should be adjusted to achieve a rate of about 2-3 bubbles per second. The rate of bubbles will vary with water depth, so during adjustment the vessel should ideally be at least half full.

Once you have the system ready to go, you will need to setup the volume measurement in the UI.

In Edit mode, click the ``` Edit Volume ``` button on the PID/Temperature probe you want to use. This will pop up a form to allow you to enter the sensor details.

![Volume Form](http://i.imgur.com/cG6UB8Z.png)

If you have a setup that uses a voltage divider to go below 1.7v MAX, you can use the BeagleBone Blacks Analog Input pins. Otherwise, you should use a 5V ADC, such as the DS2450.

The form will let you select from a drop down the DS2450 one wire addresses it finds, then you just need to put the offset (A, B, C, or D).

The ``` Add Volume ``` input is the amount of liquid in the vessel at this time. The first addition should be 0 (empty) but with the required pump running.

You can select the volume unit (Litres, US Gallons, UK Gallons) in the drop down at the bottom.

Whenever you want to add a new data point. Add water of a known amount (I use 1 US Gallon/3.8 Litre incremements), enter the amount into the volume edit form, then press update. Elsinore will take an average reading and record this to the configuration file.

You must do at least three volume measurements, ideally you should do: Empty, half full, and full as a minimum. This gives Elsinore a good range of data. If you use an uneven vessel (like a keg) then you should do as many as you can.

Now when you use the system the volume measurement will be shown for that device automatically.

Performance Enhancement
========================

The ripple present in the pressure sensor reading due to the bubbles formed with this arrangement shows up as noise in the reading. This noise typically corresponds to a variation of less than a quart; however, the BrewTroller firmware includes averaging on the volume sensors to reduce or eliminate this noise. If necessary you can fine tune the averaging logic in the Config.h of the BrewTroller
