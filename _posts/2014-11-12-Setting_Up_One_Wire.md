---
layout: page
title: How to setup one wire for your system
tagline: One Stop Shop!
description: ""
categories: Elsinore brewery raspberrypi beaglebone dto instructions setup
---

This is a catch all page that you'll probably be linked to from the startup process if Elsinore cannot find your One Wire temperature probes

### What is One Wire?

The One Wire protocol from Dallas, allows lots (up to 255 I think, but way more then Elsinore'll need) of devices to be attached to one pin. The devices are 64 bit addressed, so pin order doesn't matter.

Elsinore uses One Wire for temperature probes and volume reading.

There's a difference in setting up One Wire for Linux Kernels below 3.8 (normally RaspberryPi) and 3.8+ (normally Beaglebone)

### Linux Kernel 3.6 (RaspberryPi) (provided by Cank)

[Set up your DS18 probes](https://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/temperature/)

Then run this code in the LXTerminal to automatically load the One-Wire modules on start up

Open /etc/modules to edit

	sudo nano /etc/modules

Add these lines to the bottom of the file /etc/modules

	w1-gpio
	w1-therm

Then reboot

	sudo reboot

### Linux Kernel 3.8 (BeagleBone Black)
 
For beagleboard to get OneWire support, and GPIO control, you need to install a Device Tree Overlay file. I have added these under the support directory.

The dts file will show you the pin, but it's ```P8.11```

To compile the overlay: 

``` sudo dtc -O dtb -o /lib/firmware/w1-00A0.dtbo -b 0 -@ w1.dts ```

Or copy the w1-00A0.dtbo in the support directory to /lib/firmware (as root), the above command copies the file for you.

Login as root (such as "sudo su") and run 

``` echo w1 > /sys/devices/bone_capemgr.8/slots ```

Note: bone_capemgr.8 may be bone.capemgr.9 depending on your setup

I have provided a file which will install the One Wire (and jGPIO DTO files):

``` ./extras/w1_setup.sh ```
