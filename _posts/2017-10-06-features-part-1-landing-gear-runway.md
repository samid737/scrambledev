---
title: 'Features part 1: Landing gear, Runway, Take-off/landing'
layout: post
---

Two major features were added over the past two weeks. Take-off and landing is now fully featured. Landing succesfully is pretty challenging though!

## Landing gear

![LDG](http://g.recordit.co/QuXCkTxsmn.gif)

A landing gear is added to the spritesheet and animated in Phaser using [tweens](https://phaser.io/examples/v2/category/tweens). Tweens are basically one liners for animating sprites.  Currently the landing gear is managed automatically during the approach and take-off phase. This might as well become input driven. Extension happens at approach speeds, low altitude,  below 4.000ft. 

## Runway

![RWY]({{ site.url }}/scrambledev/assets/images/RWY.png).

A second sprite is finally added to the world. A runway is added using [tileSprites](https://phaser.io/examples/v2/category/tile-sprites) so that the length of the runway can be varied. The runway is stretched to the entire game width for now. There is no scenery involved yet, its just one infinitely stretching runway, perfect for testing purposes.
This is the second sprite with A physics body attached to it. The sprite position is fixed to the bottom of the game world.

## Take-off/landing

![GRD](https://simplescientist.files.wordpress.com/2010/10/airplane1.png)

Take-off and landing occurs when the aircraft is on the ground (the ground phase) and basically add an extra drag component  $$D_g$$ to the [equations of motion](/scrambledev/2017/04/01/development-part-xx-eom-basic-atmosphere.html):

$$D_g= \mu N + D_p$$

 where $$ N=L-W$$, the normal force, $$\mu$$ some tire friction coefficient assumed uniform for all tires ([Assumption]()), $$D_p$$, parachute drag (if equiped). 


An extra flight state check is performed during take-off and landing. Whenever the aircraft is in ground phase, inflight related functions are not executed (stall checks, speedlimits, g-limits, structural limits). During the take-off run, the flight state is switched to inflight whenever the aircraft is airborne, above $$VLOF$$. 

Impact checks are performed at touchdown:

```
function checkimpact() {
	if (myAircraft.body.velocity.y > 500) {
		resetplayer();
	}
	if(myAircraft.angle>20||myAircraft.angle<-20){
		resetplayer();
	}
	if (!LGLOCKED) {
		resetplayer();
	}
}
```

To demonstrate, A full take-off and landing run: