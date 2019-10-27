---
title: Supersonics,Object Oriented approach, sounds,
layout: post
---

I am super excited with the outcome of last week. Although the features are less spectacular and most of the development time was spent on improvements, the demonstration below shows that it was the improvements are definitely valuable.

*All updates are found in the [changelog](/scrambledev/2017/10/01/changelog.html).*

## Supersonics

The biggest problem until now was the unrealistic altitude capability. The MIG-21 has a ceiling at around 60.000ft, but the aircraft can easily reach 90.000ft right now.
The engine model, but also some assumptions  are to blaim for this. The details are found in [part 2](/scrambledev/2017/04/01/development-part-xx-eom-basic-atmosphere.html).

### Engine model revisited

About 80% of last weeks development time was spent on remodelling thrust. The first improvement incorperates speed into the current engine model.  With higher speeds , the engine mass flow increases, which could benefit the [thrust](https://www.grc.nasa.gov/www/k-12/airplane/thrsteq.html), but the intake vs exhaust velocity delta decreases.  The thrust model now incorperates the Mach number as a parameter for A more accurate engine model. 

The majority of time though was spent on researching A more sophisticated turbojet model using [this](https://web.stanford.edu/~cantwell/AA283_Course_Material/AA283_Course_Notes/AA283_Aircraft_and_Rocket_Propulsion_Ch_04_BJ_Cantwell.pdf) source as A reference. The model does seem to work, but more research is needed to succesfully incorporate it. I had to draw the line with the current model, otherwise I would spend too much time on R&D. If it works, it works. 

### Drag model revisited

I also took some time to add the effect of supersonic drag (wave drag) by adding Mach number to the parabolic drag polar, which is now:

$$\boldsymbol{C_D= C_{D0}(M) + K(M) C_L^2}$$

Typical drag variations with mach number look like:

![MACH](https://www.theairlinepilots.com/forumarchive/principlesofflight/wavedrag.jpg)

This variation is modeled as A piecewise linear function:

![PIECE](http://www.rusnauka.com/5_SWMN_2012/Matemathics/4_101389.doc.files/image109.jpg)

###### the above is not the actual model, just to illustrate.

## Object oriented code

This was probably the most exciting improvement, which was on my [TODO](/scrambledev/2017/10/01/changelog.html) list for quite some time. The code was previously not focused on reusable, extensible object oriented code. There was one aircraft class, with some key attributes, but most of the code consisted of seperate globally accessible functions.  Improving this turned out to be major, why? I urge you to check out the demonstration below to find out.

## Feel the bass

Just to fool around a bit, I made some custom aircraft sound effects. Different engine sounds are added and their volumes are adjusted to match the engine thrust setting. No pitch adjustments unfortunately....not yet at least. Idle sounds, full power, afterburner thrust are added. A nice [soundtrack](https://www.youtube.com/watch?v=L9epcjTej7E) is also added to the video below just to spice things up (THIS WILL NOT ADDED TO THE GAME). A stall warning beep sound is also added.

## Mission

Progress is demonstrated.

### Briefing

![m01]({{ site.url }}/scrambledev/assets/images/manouvres/02.png)

Initial altitude 30.000ft, speed 350KTS. The flight leader is flying with you, so try to keep up with your leader. Finally, break away.

### Flight

<iframe width="560" height="315" src="https://www.youtube.com/embed/WTg3_xKTTW0?rel=0" frameborder="0" gesture="media" allowfullscreen></iframe>

Forget about my piloting skills for now, but as you can see, restructuring to object oriented code allows you to add more aircraft to the simulation! Pretty neat  right?! The second aircraft is completely autonomous and has the autopilot engaged. However, it lacks a pilot (AI), so it cannot fly without the autopilot engaged. I also decided to change the camera tracking logic to always track the player.

*Scramble JS uses Phaser 2 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*