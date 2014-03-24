---
layout: page
title: "BeagleBone Black Setup"
tagline: "BBB is lovely"
---


The [Beaglebone Black](http://beagleboard.org/Products/BeagleBone+Black) is similar to the Raspberry Pi, but with more GPIO and onboard Analogue in (that has a max of 1.8V)

# WARNING

**It is highly recommended you setup a KILL SWITCH that will terminate the negative and/or the positive to the SSRs. This is a safety feature and allows you to kill the SSRs without going through the UI**


### Launching

You _must_ set the "Gpio_definitions" property on launch 

``` java -Dgpio_definitions=extras/beaglebone.json -jar Elsinore.jar ```

Otherwise the system will error

### GPIO Naming

The Pinout number is different between RaspberryPi and Beaglebone.

For Beagleboard Black Pinout: http://elinux.org/BeagleBone#P9_and_P8_-_Each_2x23_pins

BeagleboardBlack has multiple banks, for example GPIO2_2, this translates to physical pin 66, banks are separated by 32 outputs per bank. 


### Overlays

For beagleboard to get OneWire support, and GPIO control, you need to install a Device Tree Overlay file. I have added these under the support directory:

To compile the overlay: 

``` sudo dtc -O dtb -o /lib/firmware/w1-00A0.dtbo -b 0 -@ w1-00A0.dtbo ```

Or copy the w1-00A0.dtbo in the support directory to /lib/firmware (as root), the above command copies the file for you.

Login as root (such as "sudo su") and run 

``` echo w1 > /sys/devices/bone_capemgr.8/slots ```

Note: bone_capemgr.8 may be bone.capemgr.9 depending on your setup

I have also provided a sample jGPIO created overlay for GPIO0_7 as a pinout (jgpio-00A0.dtbo) which can be used in the same was as above

``` sudo cp extras/jgpio-00A0.dtbo /lib/firmware/ ```

``` echo jgpio > /sys/devices/bone_capemgr.8/slots ```

#### jGPIO

[jGPIO](http://dougedey.github.io/jGPIO/) is a Java application I made to generate the Device Tree Overlays based on a JSON configuration file. At the time of writing this affects Linux Kernel 3.8 and above. The raspberry Pi doesn't support Kernel 3.8 yet.

### Creating a custom Overlay

If you want to create a DTC file for custom GPIO pinout, you can read the instructions in the [jGPIO](https://github.com/DougEdey/jGPIO) repository

But the synopsis is

``` java -cp Elsinore.jar -Dgpio_definition=extras/beaglebone.json jGPIO.DTOTest <List of GPIO pins> ```

For example

``` java -cp Elsinore.jar -Dgpio_definition=extras/beaglebone.json jGPIO.DTOTest GPIO0_7 ``` 

Will recreate the default GPIO0_7 file as jGPIO-00A0.dto, you will then need to compile this as the same as above but for jgpio
 
``` sudo dtc -O dtb -o /lib/firmware/jgpio-00A0.dtbo -b 0 -@ jgpio-00A0.dto ```


### Analogue inputs

There is already a precompiled AIN DTO for the Beaglebone Black, BB-ADC, as above:

``` echo BB-ADC > /sys/devices/bone_capemgr.8/slots ```

To Activate them.



