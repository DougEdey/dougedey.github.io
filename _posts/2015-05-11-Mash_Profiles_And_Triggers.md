---
layout: page
title: Triggers & Profiles
tagline: "How to use the Recipe Upload and Trigger Profiles"
description: ""
categories: Elsinore java strangebrew brewery beer controller triggers mash
---
{% include JB/setup %}

Why Do You Need To Write This?
==========================

The trigger interface has evolved recently and I feel it's needed (since I don't get paid, I want to not answer questions).

What's Changed?
==================

Some minor tweaks have been made with regards to activating and deactivating the profile. But this will give you a quick walkthrough of how to set a trigger profile and how it works.

Settings UP A Trigger Profile
==================

So, there's two ways to set up a trigger profile. The first, is a manual process where you add new triggers, re-arrange, set them up, and make sure you're happy. This gives you more flexibility, but it's not the easiest way to do things.

That's why I added Recipe Upload. When you upload a recipe, you'll be able to view the Mash or Hop Additions profiles, then you can select which temperature probe, or PID to set up the Profile for. When you've selected the target sensor and the page is reloaded, you'll be able to see the Trigger Profile is setup for that probe.

OK, That's Easy. How Do I Activate it? How Do I Deactivate It? WHAT HAPPENS DUDE?! TELL ME! I NEED TO KNOW!!!!!!ONEONEELEVEN!
======================

So, here's a basic example with how the profiles work, using a real world example taken from a user on HBT

```
Dough-in at 133F
wait for 15 minutes
raise to 152F
hold for 60 minutes
raise to 170F
```

You will get a Trigger profile of:

```
Temperature Trigger: 133F
Wait Trigger: 15 mins
Temperature Trigger 152F
Wait Trigger: 60 mins
Temperature Trigger: 170F
```

When you press "Activate"

The PID will set to 133F as the target temperature, and will be automatically set to "Auto"

When 133F (+-2F) is hit, the Wait Trigger will activate.

15 minutes later, the wait trigger will deactivate.

The next Temperature Trigger will activate, set the PID target temperature to 152F.

When 152F (+/-2F) is hit, the next wait trigger will activate.

60 minutes later, the wait trigger will deactivate.

The next Temperature Trigger will activate, set the PID target temperature to 170F.
