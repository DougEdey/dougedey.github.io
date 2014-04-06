---
layout: page
title: "Mash Profiles"
tagline: "StrangeBrew and Mash Profiles"
---

So I have spent a week getting __Mash Profiles__ working in [StrangeBrew Elsinore](http://dougedey.github.io/SB_Elsinore_Server/), it's at a point now where I feel comfortable allowing other people to __TEST__ this functionality (I don't use it in my setup personally)

# This is a TEST Feature

If you see an issue, please raise a bug with as much information as possible. One line "This doesn't work" won't help me to fix it. Check the logs, this feature has lots of WARNING output (rather than info) until it's been tested well enough to be part of the main branch.

### What is a Mash Profile?

I know I'm probably not using the right phrase, but I figured it was catchy enough to refer to, and it gets the intent of the feature across.

A Mash Profile is a series of Mash Steps, many Mash Steps equal one Mash Profile.

In Elsinore, you can have a mash profile for each PID you have setup.

### OK, what does a Mash Profile allow me to do?

The profile allows you to setup mash steps in advance, with target start temperatures, duration, and names, Elsinore then has a background thread for each Mash Profile that has been setup.

What Elsinore does is:

1. Checks to see if there's an active mash step, if there's not it doesn't do anything, simple.A
1. Sets the target PID Temperature to that of the mash profile
1. Checks to see if the current temperature on the profiles PID to see if it's in range of the target profile (currently this is hard set to +/-2F, but this is next on my list to make flexible)
1. If it's within the target range, it will then activate the mash step and set the start time, whilst at the same time setting the target end time
1. If the end time has been hit, or surpassed, the actual end time is recorded (up to 10s difference)
1. If there's another mash step, this becomes the active step
1. Goto (1)

### Sweet, it's like a set and forget thing!

__No__, seriously it's not, you need to monitor everything closesly, as I said at the beginning, I don't use this feature (at the moment) so it's difficult for me to detect any issues.

Also, whilst Elsinore does set the Target Temperature, it does NOT activate the element by itself. If a PID is already on manual, it will not move it to Auto, or Off. I don't want to active an element when someone hasn't put their water in, or something isn't right!

### OK, I get it, I think I want to use this.

Cool, I like you already. But this isn't something you can do with Elsinore by itself.

You'll need to use [StrangeBrewQT](http://dougedey.github.io/StrangeBrewQT/) to use this feature.

When you get StrangeBrewQT, you can build it from source (install QTCreator and hit build, it should work on all platforms), using the _elsinore_mash_ branch. There's a post __TO_COME__ with links to binary drops for Mac/Windows/Linux as standalone archives. Sorry, I don't have an automated build system for all of this yet.

When you have your recipe and mash profile setup in StrangeBrewQT, under the tools item there's a "Send Mash" option under "Tools", this will attempt to send the mash profile to the Elsinore Server you have setup under Preferences->Brewer.

You'll get relevant messages for any issues that StrangeBrew finds when trying to update the mash Profile, and then a message for the profile being sent

You will see a prompt to select the relevant PID that you want to acivate the mash profile for. 

If there's a profile already active, you can override it!

![Elsinore on](https://raw.githubusercontent.com/DougEdey/dougedey.github.io/master/assets/images/mash_profiles/elsinore_on.png)
![Elsinore Support](https://raw.githubusercontent.com/DougEdey/dougedey.github.io/master/assets/images/mash_profiles/SB_Mash.png)
![Elsinore Sent](https://raw.githubusercontent.com/DougEdey/dougedey.github.io/master/assets/images/mash_profiles/to_elsinore.png)

### It's Sent! What next?

In the Web interface, the relevant PID will show a table of the mash steps, by default none are activated.

![Mashstep View](https://raw.githubusercontent.com/DougEdey/dougedey.github.io/master/assets/images/mash_profiles/mashstep_activate.png)

So you'll need to click the "Activate" button when you're setup to go. Then press "Auto" on the PID to activate the element.

![Mashstep Active](https://raw.githubusercontent.com/DougEdey/dougedey.github.io/master/assets/images/mash_profiles/mashstep_enabled.png)

When the PID temperature is within the target range, +/-2F by default, the timer will start

![Mashstep Timer](https://raw.githubusercontent.com/DougEdey/dougedey.github.io/master/assets/images/mash_profiles/timersmash.png)
