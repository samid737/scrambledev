---
title: Autopilot controller, pitch limiter
layout: post
---

Last week  was mostly spent on writing aboutthe  early stage developments (starting  [here](/scrambledev/2017/03/01/progress-part-1-flight-mechanics-physics-system-world-setup.html)), so it  was kind of A recap on everything I've done so far.  I want the updates to be helpful to readers so I try  to take my time writing each part. This is why there is A noticeable gap in the post timeline.

Adding an autopilot was not on the list of features at first.  While analysing and endlessly recalibrating the aircraft in its stability (read more in [Modeling part 3: Stability and Control](/scrambledev/2017/05/01/development-part-4-modeling-thrust-basic-control.html)) I figured that having an autopilot would help out substantially. In [part 3](/scrambledev/2017/05/01/development-part-4-modeling-thrust-basic-control.html) I also mentioned the control output to be dangerously sensitive, providing immediate response and ignoring the airframe and pilot limits. This makes it harder to properly calibrate the aircraft. The pitch limiter solves this problem.

*All updates are found in the [changelog](/scrambledev/2017/10/01/changelog.html).*

## Autopilot control system

The Autopilot currently supports two modes:

- speed hold/autothrottle
- altitude hold

For both cases, A [PID controller](https://www.npmjs.com/package/node-pid-controller) is implemented. [Here](http://www.flightgear.org/Docs/XMLAutopilot/node2.html) is a nice read on how A PID is used in autpilot systems, it definitely helped me out.

Just like most autopilots, there is A master hold switch and individiual hold switch. The GUI is not yet implemented, everything is in [dat.gui](http://workshop.chromeexperiments.com/examples/gui/#1--Basic-Usage). The autopilot altitude hold still needs to be fine tuned by ajdusting the gains, but it will eventually hold at near reference altitude (there is some total error).

## Pitch limiter

The pitch limiter is an inverse proportional controller. It reduces the actual elevator deflection with increase in load factor and uses the ultimate design load factor  as A reference value. 

```
var x = Phaser.Math.clamp(Math.abs(myAircraft.n / myAircraft.nmax), 0.1, 1);
myAircraft.limiter = 1 / (myAircraft.limiterGain * x + 0.1);

//in control input function
myAircraft.elevator.angle = pitchValue * 15 * myAircraft.direction * myAircraft.limiter;
```

## Mission
The autopilot is demonstrated.

### Briefing

Initial altitude 10.000ft, 450 KTAS. Autopilot master switch is enabled during start. Hold is set at 15.000ft , 450KTAS.

### Flight

<iframe width="560" height="315" src="https://www.youtube.com/embed/tRIJSTOKwGg?rel=0" frameborder="0" gesture="media" allowfullscreen></iframe>

Notice how the holding altitude is currently off by A couple of hundred feet. The autopilot still needs some fine tuning. Speed is controlled by adjusting throttle output, hence the only way to slow down is by pushing the throttle back.