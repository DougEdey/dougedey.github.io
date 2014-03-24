---
layout: page
title: Raspberry Pi Basic Setup for StrangeBrew Elsinore
tagline: "Thanks to Cank!"
description: ""
---

This is very kindly provided by [HBT User Cank](http://www.homebrewtalk.com/f170/raspberry-pi-strangebrew-elsinore-basic-setup-463590/)

### Setup the Operating System

[Download and install latest NOOBS](http://www.raspberrypi.org/downloads)

Install Raspbian Operating system and set it up based on your location.

### Setup the Hardware

[Set up your DS18 probes](https://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/temperature/)

Then run this code in the LXTerminal to automatically load the One-Wire modules on start up

Open /etc/modules to edit

	sudo nano /etc/modules

Add these lines to the bottom of the file /etc/modules

	w1-gpio
	w1-therm

Then reboot

	sudo reboot

### Download Elsinore

Download the SB_Elsinore_Server from git

	git clone https://github.com/DougEdey/SB_Elsinore_Server.git ~/BrewServer

Switch directories

	cd ~/BrewServer

Run Elsinore

	sudo java -jar Elsinore.jar

### Choosing the GPIO Pins
See this [post](http://www.homebrewtalk.com/f170/raspberry-pi-strangebrew-elsinore-basic-setup-463590/index3.html#post5986888) to make sure you use the correct GPIO pins for output and you don't choose one that is in the default HIGH state when the Pi boots up!!!

**It is highly recommended you setup a KILL SWITCH that will terminate the negative and/or the positive to the SSRs. This is a safety feature and allows you to kill the SSRs without going through the UI**

### First time setup

It will run some lines of code then show a list of your sensors and ask you to:

	Select the input, enter "r" to refresh, or use "pump &ltname&gt &ltgpio&gt" to add a pump
	Type "volume" to start volume calibration
	Type "timer &ltname&gt" to add a timer

![Initial Setup](http://cdn.homebrewtalk.com/attachments/f170/183770d1394036656-raspberry-pi-strangebrew-elsinore-basic-setup-elsinoresetup1.jpg)

### Some errors

If you see

	"java.net.ConnectException: Connection refused"

This means Elsinore is looking for OWFS (the full stacktrace will have OWFS in it) and OWFS isn't enabled on your system. There was a bug that caused this after restarting Elsinore. This has been [fixed](https://github.com/DougEdey/SB_Elsinore_Server/commit/443ad3b69d6100db73b2afe9af37d749e3b4a860). 

If you get an error at this point saying it can't see your sensor check out this [post](http://www.homebrewtalk.com/f170/raspberry-pi-strangebrew-elsinore-basic-setup-463590/#post5969791).

It might ask you about switching to OWFS. Say No.

### Setting up the System

At this point enter the number of the sensor you want to set up and hit enter. (I only had one so I entered "1" and hit enter.
It will ask you to name it. (I named mine "HLT")
Then it ask you what GPIO output the SSR is hooked up to so it knows which pin to turn on and off based on the Temperature reading or your sensor. 
I used "GPIO27" which is pin 13
If you just want a temperature reading, say for mash tun or cooled wort, leave it blank and hit enter.
I then typed

	timer Mash
	timer Boil
	pump Pump1 GPIO22

	quit

![Setup an output](http://cdn.homebrewtalk.com/attachments/f170/183771d1394036656-raspberry-pi-strangebrew-elsinore-basic-setup-elsinoresetup2.jpg)

It will tell you:

	Updating config file, please check it in elsinore.cfg.new
	Config file updated. Please copy it from rpibrew.cfg.new to rpibrew.cfg to use the data
	You may need to do this as root
	Saving HLT with probe 28-00000XXXXXX
	Creating element of general
	Creating on configDoc base

### Copying the config file

If it didn't create this last file, type this:

	cp elsinore.cfg.new elsinore.cfg

### Running and using Elsinore

Then run:

	sudo java -jar Elsinore.jar

and in a web browser go to the Raspberry Pi IP address

	192.168.1.XX:8080/controller

You should see:
![Web Interface](http://cdn.homebrewtalk.com/attachments/f170/183772d1394036656-raspberry-pi-strangebrew-elsinore-basic-setup-elsinore3.jpg)

### Stopping elsinore

Stops the application

	Ctrl-C


The last photo is of a breadboard that I have leds hooked to my gpio output pins for the pump(green led) and the HLT ssr(white led) when I turn the pump on the green light comes on, when I send a command for the HLT it turns the white led on based on duty cycle.
Pretty sweet!!!

![Breadboard](http://cdn.homebrewtalk.com/attachments/f170/183773d1394036656-raspberry-pi-strangebrew-elsinore-basic-setup-img_4392-1-.jpg)
