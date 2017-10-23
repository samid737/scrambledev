---
title: 'Development part X: Head up display, Secondary flight controls'
layout: post
---

Last week I worked on two features that are extremely valuable to the user:

##  Head up display (HUD).

![display]({{ site.url }}/scrambledev/blob/gh-pages/assets/images/screenshots/HUD1.png)

The HUD is pretty similar to the one used in [Aero Elite Combat academy](https://i.ytimg.com/vi/bBFGRPCQngE/maxresdefault.jpg), A minimalistic HUD. It provides all the essential flight information for combat aircraft flight, leaving out all the flight systems that can [fill](https://i.ytimg.com/vi/1UrF6bmwe_E/maxresdefault.jpg) up the entire display field. The sim is in 2D in longitudinal direction, therefore heading display is removed and the pitch ladder is locked to pitch motion.

Flight info included:

* Pitch
* True airspeed
* Mach
* G load
* Altitude
* Throttle commanded
* Throttle output
* Yoke input
* Secondary flight control indicators: flaps, speedbrakes
* Airframe stress/damage
* Fuel indicator
* Weapon indicators (yet to decide)


##  Secondary flight controls.

### High lift devices
I played around and tried to land and take-off with the current state of the flight model and I was quickly able to confirm the difficulties that arise with low-speed flight for high speed aircraft This also proved the flight model has a pretty high level of accuracy. The angle of attack can increase to A critical angle when lowering speed at A steady (low) altitude, resulting in low speed stall. Without high lift devices, there is no mechanism to deal with such critical angle of attack. The player must be able to Take off and land, so it was necessary to consider high lift devices.  
Flaps will be the available as A high lift device. Flaps will influence the lift coefficient by increasing it at the same angle of attack .  This will allow the user deal with low-speeds well within angle of attack margins. [This](https://ieeenitk.org/blog/High-Lift-devices/) article explains it briefly. 

The aircraft is assumed to have two flap settings, with two coefficients that will be added to the lift coefficient whenever flaps are deployed. The pseudocode:

```
//in aircraft setup:
aircraft.flaps1 = 0.01;
aircraft.flaps2 = 0.02;

if(flapSetting == 1){
  CL= CL + aircraft.flaps1;
  CD += smallnumber;
}
		
if(flapSetting ==2){
  CL= CL + aircraft.flaps2;
	CD += smallnumber;
}
```

### Airbrakes

![]({{ site.url }}/scrambledev/blob/gh-pages/assets/images/screenshots/AIRBRAKE.png)

[Airbrakes](http://c8.alamy.com/comp/D4RX54/a-serbian-air-force-mig-21um-jet-fighter-with-air-brakes-in-flight-D4RX54.jpg) are necessary to slow down the aircraft and are also iplemented. They basically increase overall drag. Similar to how the flaps increase the CL value, deploying airbrakes will add some predefined constant to the drag coefficient of the aircraft.

*Scramble JS uses Phaser 2 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*