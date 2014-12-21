---
layout: page
title: StrangeBrew Elsinore
tagline: "An Opensource Brewery Controller"
description: ""
categories: elsinore setup instructions beaglebone raspberrypi
---
{% include JB/setup %}

Strangebrew Elsinore Server
==================


Java Server for Strangebrew Elsinore

The purpose of this project is to create a Java application that can run on small systems such as the RaspberryPi and the Beaglebone series

Since these systems run on Linux, that is a requirement to using this.

The system is based off the Dallas One Wire protocol for the temperature probes (expanding to analogue inputs too), and Straightforward GPIO outputs for SSR control

Setup Instructions
====================
[Beaglebone Black](extras/BeagleboneBlackSetup.md)

[RaspberryPi](extras/RaspberryPiSetup.md)

The above instructions will tell you how to setup your systems for Elsinore

Startup Instructions
====================

Clone this repository:

``` git clone https://github.com/DougEdey/SB_Elsinore_Server ```

Move to the checked out Directory:

``` cd SB_Elsinore_Server ```

Run:

``` ./launch.sh ```

Wait, what happened to the old instructions? Well I found that people weren't following them well. So I rewrote the UI, you can now setup everything (almost) from the UI.

If you have a DS2450 (or don't want to use Analogue inputs for reading the volume, BBB is 1.7V so not very good for reading the analogue inputs. You will see a request for OWFS, please use OWFS if you can, it's better in general.


~~~
./launch.sh 
Starting Elsinore as elsinore
[sudo] password for elsinore: 
May 17, 2014 8:29:23 PM com.sb.elsinore.LaunchControl main
INFO: Running Brewery Controller.
CFG IS NULL
DOC IS NULL
Detected a non temp probe.20-00000008dc9e
Do you want to switch to OWFS? [y/N]
y
Creating the OWFS configuration.
What is the OWFS server host? (Defaults to localhost)

What is the OWFS server port? (Defaults to 4304)
~~~

Then you can use the web UI.

Web UI
======

The standard view you'll see at the start is an un-named display, such as:

![Initial Setup View](http://i.imgur.com/61lm1VI.png)

The probe "names" are their addresses, double clicking them allows you to set them up

* You can set just the name (which will leave it as a temperature probe)
* A GPIO pin (which will set it up as a PID controller)
* And if you use a GPIO Pin you can set an Aux pin at the same time, allowing you to use an auxilliary ouput.

![Setup Probe](http://i.imgur.com/FSAxuYB.png)

Volume Reading
==============

Volume reading can be done using any analogue input, I personally used the same hardware as [Brewtroller](https://www.oscsys.com/projects/brewtroller/system-design/volume-measurement) connected to a one wire DS2450, this allows it to connect to the one wire bus.

[More indepth documentation](http://dougedey.github.io/2014/12/20/Volume_Setup)

RaspberryPi or Beagleboard?
=======================

The BeagleBoard Black does have a big advantage over the RPi, it has onboard analogue inputs, but these are 1.8V.

The RaspberryPi works fine with the existing software, the only thing you need to do differently is naming the GPIO Pinouts.

One Wire & OWFS
==========
One Wire is fantastic (in my opinion) each sensor or device has a full 64 bit address, and you don't have to worry about the order and you can chain them!

One Wire devices can be chained, with only one Pullup resistor before the first connection to a device. I currently have 4 Temperature probes on my circuit, and a ADC, connected using XLR jacks.


[OWFS](http://owfs.org/) is a much better One Wire Implementation, it is highly recommended to install it, and it is REQUIRED if you use One Wire based Analog inputs (like the DS2450

Install it using your standard package manager, then you need to set a mountpoint up (I use /mnt/1wire) and set 

``` server: w1 ``` in the OWFS configuration File (/etc/owfs.conf by default), you can chose the ports as you want for OWFSHTTP and OWServer, the configuration tool will setup OWFS if it can.

To manually setup OWFS, use the option -owfs when starting up Elsinore

Cutoff Temperature
============
After the [incident](http://imgur.com/a/pwQVE) I decided to add a cutoff temperature, in my case I have a temperature probe on my SSRs, and when they go over a certain temperature I want to kill the server so it doesn't get badly damaged

This is to come in the updated Web UI setup.

System Temperature
============

System can be enabled during setup by entering "system" (no quotes) at the prompt.

Also, to enable the System Temperature reading, please add

``` <system /> ```

In the ``` <general> ``` section of the configuration file.

Timers
=========

Use the web UI, click on "Add Timer" to create a timer.

Pump Control
============

To add a pump, use the "Add Pump" button on the Web Interface

Config File
=========

This is now automatically controlled, you shouldn't need to do anything to it, except for backing it up.

Control Interface
============

Visit 
```
<ip of your system>:8080/controller
```
to access the webUI, which works on mobiles too:

![Browser Layout](http://i.imgur.com/j59BcFZ.png)

[Album of the UI Progress](http://imgur.com/a/jEIbc)

This is an example of the PID control interface, temperature probes are displayed on the right hand side as LCD displays. On the Raspberry Pi you'll also get the system temperature (this isn't enabled on Beagleboard yet)

There is also a Android Application which is not currently in development, search my repositories to check this, but it's not deprecated yet, I haven't changed the JSON output from the system so it should continue to work.

Thanks For reading this, if you have any queries please contact me or file a bug.
