---
layout: page
title: "Required Hardware"
tagline: "Remember: Safety first!"
---

### The list!

To begin with, I must state: Be careful when doing anything, you're going to be turning electrcity into heat, there will invariably be some bare wires around whilst you're doing things, these may kill you.

You want to have a GFCI circuit for anything that's going to be around water, either with a GFCI breaker on your Fuse Panel, or a GFCI cable for the mains current.

### The List! (Really)

You can break down the system into various components, the controller itself, the temperature probes, the volume sensors, the heating elements, etc...

## The Controller

You'll need a [Raspberry Pi](http://www.raspberrypi.org/) or a [BeagleBone Black](http://beagleboard.org/black) these are both Linux based (by default) systems that have GPIO Output. 

You'll need to install an Operating System, I personally use Ubuntu, and the guides have been written with Ubuntu in mind. But anything with a One Wire module will work (see the next section).

## One Wire

One wire is a system that allows multiple devices to use a single pin, and they're 64 bit addressed so you don't need to put them in any physical order.

For this you need:

 * A 4k7 Ohm resistor
 * DS18B20 (or any compatible temperature sensor)
 * Some wires
 * XLR jacks and sockets (optional, but it makes it easier to move around and change)

(I'll add more information in the future, but Adafruit have a great [guide](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-11-ds18b20-temperature-sensing/overview) for getting started.

Make sure you get waterproof temperature sensors to go in the kettle, you can use the Electric Breweries guides for this, just replace the PID temperature probes with the One Wire ones.

## The Kettles/Elements

[The Electric Brewery](http://theelectricbrewery.com/) has incredibly indepth guides for all this stuff, I recommend you use their guides (and their kits if you want to make things easier). But don't get the PIDs. Elsinore replaces all the PIDs for you

## Special instructions for Elsinore

You don't need LEDs (though they're a good idea on the hot side so you know when the elements are live).
You should have physical overrides, such as a switch on the GPIO side of the SSRs, just a switch to open the circuit so they turn off.



