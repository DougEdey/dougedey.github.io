---
layout: page
title : "Dougs Pages"
tagline : "About the projects"
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## About Me
I'm a Software Developer based in Ottawa, Ontario, I emigrated from the UK in 2010 whilst working for IBM in the JTC. 

My core experience comes from working within IBM in the Systems Technology Group performing hardware bringup and testing, before moving to the Software Group with the Java Technology Center.
Working in the JTC as a L3 Software Support Developer exposed me to a lot of different usage paradigms, and working with people who write the Java Virtual Machine, and helping to fix issues, both with applications running on the JVM and within the JVM itself. 
After a few years of working for IBM I decided that I wasn't feeling fulfilled in my role and moved to a significantly smaller company in Ottawa, 360pi, as the person with lower level knowledge.
360pi underwent a restructuring in Summer 2014 to focus on sales, and I moved on to work for Alcatel-Lucent as a SAM Software Designer. In this role I work on the core platform and have gained a large amount of experience with JBoss, networking, and large source code repositories.

I find learning about the intricities of products to be extremely fulfilling, this is why I write software, knowing that I understand a product, and it's inner workings.

## StrangeBrew
I started homebrewing beer in 2011, and I took over control of the [StrangeBrew](http://dougedey.github.io/StrangeBrew) recipe tool from Drew Avis. This was because of my desire to push it forward and fix issues within it. I liked it because of the write-once ability of Java (mostly).

## StrangeBrew Elsinore
In 2012 I started work on [StrangeBrew Elsinore](http://dougedey.github.io/SB_Elsinore_Server/), as a standlone, open source piece of software that allows control of electric homebrewing setups. With no scalability limits. Running on Beaglebone Black and Raspberry Pi. A HBT User helped me to get some [Raspberry Pi Documentation](http://dougedey.github.io/2014/03/22/Raspberry-Pi-Basic-Setup/) written

## jGPIO
Whilst writing StrangeBrew Elsinore for the Beaglebone Black, I discovered that Linux Kernel 3.8 used something called Device Tree Overlays, these are not the easiest thing to understand, but it requires custom files to be written and compiled before the GPIO/Pinouts can be used by application. So I wrote a Java based application that generates the files, aswell as provide a support library for Java that allows Java access to pins. It's not feature complete (I haven't added PWM yet) but it allows digital and analogue I/O. I wrote my own because I found limitations by other available libraries.

Hence, [jGPIO](http://dougedey.github.io/jGPIO) was born.

## SB Elsinore Android
Whilst writing Strangebrew Elsinore, I decided to play with Android application writing, and I wrote a [native application](http://dougedey.github.io/SB_Elsinore_Android) for Android. Whilst I no longer actively maintain this, it provided me with good experience in writing Android Applications.

It currently is behind in that it doesn't support the new timer model, or pumps, or auxilliary controls. But it's not infeasible to update the application

## StrangeBrew QT

In 2014, as a result of some work I'd done using QT at work, for making a web renderer, as well as a [talk](http://mirror.linux.org.au/linux.conf.au/2014/Thursday/83-Gtk_to_Qt_-_a_strange_journey_-_Dirk_Hohndel.mp4) by Dirk Hondel about porting Subsurface from GTK to QT, made me decide that StrangeBrew needed a native look. Java Swing never looked natural whenever I used it. But QT allows the write once, run many times methodology to work with C++ code. Just requiring some makefile, and compiler specific changes. In the span of a month, I completely rewrote StrangeBrew for QT. Producing [StrangeBrew QT](http://dougedey.github.io/StrangeBrewQT/). 

There's been a few minor issues, but it works on Windows, Mac, and Linux (at the time of writing).




