---
title: OOP , Camera target, HUD switch, Trimtabs,
layout: post
---

Ohhh yeah I cannot wait to publish this log. I must confess that the pace was A bit slower last week, but I made some extremely important internal modifications providing tremendous new possibilities. 

*All updates are found in the [changelog](/scrambledev/2017/10/01/changelog.html).*

## OOP

The [previous log](/scrambledev/2017/11/13/object-oriented-aircraft-model-sounds-engine-model.html) mentioned  the Object oriented approach. Basically I continued this approach and tried to respecify more aspects of the code.  The aircraft has some pretty heavy OO code under the hood, where almost every system is split up into components. The landing gear, structures, engine etc. are all  decomposed and having them as seperate objects adds some very unique benefits. For example, different [engines](https://www.grc.nasa.gov/www/k-12/UEET/StudentSite/engines.html) fit an aircraft and with the new code , each engine can be implemented. The turboshaft would for example fit A helicopter, so the model would need helicopter dynamics. The new code structure allows for definition of different aircraft, such as an airplane, helicopter, balloon etc. The dynamics of these aircraft is missing right now though.

## Camera target, HUD Switch

The HUD is partially decomposed and some parts of the code (especially drawing bars and text) is still procedural.  The HUD can now track different aircraft by switching data sources. Adding camera targeting provides A fully functional view switch:

<iframe width="560" height="315" src="https://www.youtube.com/embed/DYIWDuXsNAA" frameborder="0" gesture="media" allowfullscreen></iframe>

This is not limited to aircraft, so ground objects, missiles and other objects can also be tracked, but they don't exist yet.

## Trimtabs
It is now completely possible to add A wing surface of any size, shape (theoretical shape that is) at any location. This provides the possibility to add [canards](http://www.boldmethod.com/images/learn-to-fly/aircraft-systems/canards/primary-eurofighter.jpg), elevators, flaps, and  trim devices such as trim tabs:

<iframe width="560" height="315" src="https://www.youtube.com/embed/AYJOnxcYpjA" frameborder="0" gesture="media" allowfullscreen></iframe>

This features kind of gives you A hint at what I'm up to next , since large airplanes use trim devices  to reduce the amount of input required by the pilot using the elevator. It would be A perfect test of the above advances.

*Scramble JS uses Phaser 2 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*