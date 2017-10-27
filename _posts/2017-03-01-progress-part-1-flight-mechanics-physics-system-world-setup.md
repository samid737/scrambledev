---
title: 'Development part 1: Modeling Aircraft, physics system, world.'
layout: post
---

*Please not that these features where implemented in the early stage, prior to  logging the progress.  Not all details are included.*

The first objective is to model the aircraft so that it can exist inside the game engine. This way there will be at least one object to play around with. Then the phyiscs system must be considered . The simulated world must be propertly configured for the simulation to work.

## Modeling aircraft

### Sprite building

Once the [overall aircraft design ](/scrambledev/2017/01/16/aircraft-design-part-1.html) is complete, the MIG21 is split up into components and  A spritesheet is made using [TexturePacker](https://www.codeandweb.com/texturepacker). Phaser allows for hierarcichal setup of sprites. The parent sprite is the main body/fuselage, while other components (landing gear, elevators etc.) are set as [child sprites](https://phaser.io/examples/v2/sprites/child-sprites).

### Extending A Phaser Sprite

Scramble JS uses an object oriented approach to model the aircraft. It is treated as an object having numerous properties (length, wingspan, engine power etc.) and methods (retract landing gear, adjust throttle) that define the object and also determine the state of the object. Phaser facilitates this approach by allowing further extension/customization of the existing Phaser.Sprite class. The implemention in Phaser is done by extending the [Phaser.Sprite ](https://phaser.io/examples/v2/sprites/extending-sprite-demo-2)object with custom properties and creating A new instance of that specific object. 

### Properties and methods considered

The Aircraft object continously changes and so the class object code  is not provided. Conceptually, the following is considered in defining the aircraft:

#### Properties

- Aircraft dimensions
  - wingspan
  - length
  - height
- Aerodynamics
  - lift coefficients
  - drag coefficients
  - maximum angle of attack
- Propulsion
  - engine thrust
  - number of engines
- Operating limits
  - operating weights
  - centre of gravity limtis
  - speed limits, (vlof, vstall, vlg,vmax)
- input & Control
  - maximum elevator deflection
  - type of  control system (mechanics, hydraulic)
  - pitch limitation
- Autopilot related properties     

#### Methods

-  Input & control
   - landing gear retraction, extension
   - flight control input
   - autopilot controller
   - throttle control
- Flight state checks:
   -	stall
	 -  supersonic flight
	 - approach check
	 - pilot g limits
	 - structural limits

## Physics system
At this point, there is no physics involved,  just A sprite placed somewhere inside the game world. By using Phaser its [arcade physics](https://phaser.io/examples/v2/category/arcade-physics) system, we can begin giving some physical sense to the aircraft sprite (inside Phaser). The aircraft is considered to be A single rigidbody ([Assumption](#)). For now, supersonics are not considered. A subsonic aircaft is modeled, calibrated, tested first and if necessary (the approximation errors are intolerable), we consider supersonic flight.  

### Built in properties
Arcade physics is perfectly suitable for rigidbody dynamics and we can rotate and translate the aircraft using the following physics properties:

*  acceleration.
*  velocity.
*  position.
*  angularAcceleration.
*  angularVelocity.
*  rotation.

### Collision detection
Arcade Physics collision detection is based upon Axis aligned bounding box (AABB) collision detection. For this game, collision detection is required for the following scenarios:

* ground impact.
* bullets/missile impact
* mid air collision.

Arcade Physics collision detection is therefore sufficient. The more advanced [P2 Physics system](https://phaser.io/examples/v2/category/p2-physics) will not be necessary.

## World setup

Scramble JS will be viewed from the side view and the world is 2D, similar to UN Squadron for the SNES **(CLICK IMAGE FOR VIDEO)**:

[![CLICK FOR VIDEO]({{ site.url }}/scrambledev/assets/images/UN.png)](https://www.youtube.com/watch?v=-C6V_bEmOEQ&t=608s)

The frame of refence is pretty tricky to implement. In UN Squadron, the player can move around, but is bounded by the viewport and all objects are moving towards the player. This works fine for arcade/action gameplay, but for flight simulation, it will make less sense. The game world is simulated using real world dimensions (everything is in SI units) and the level of action is not like in UN Squadron. 

The player can move around freely inside A simulated 2D world. In Phaser, you can set the size of your game world using A function called setBounds(). A simulated world is setup by adjusting the world size to some  large (but not infinite) size. Since combat aircraft fly below the  [stratosphere](http://www.online-sciences.com/wp-content/uploads/2014/09/stratosphere-layer-11.jpg),  the height of the world will be less than the height of the stratosphere [ Assumption](#). I still have to think about A solution for the width of the world. It may be fixed, but could also vary with each mission.

You can also let the main camera follow the player. The main camera follows the player only when it is in the vicinity of any scenery object. When there is no action, it will not follow the player, but the world position of the aircraft is still tracked. To illustrate:

TODO

## Result

At this point there is nothing exciting going on (yet),  just an aircraft assembled and A sky gradient. For debugging purposes, the [arcade physics debug  plugin](https://github.com/samme/phaser-plugin-debug-arcade-physics) is used. This plugin displays velocity and acceleration vectors of any physics body in Phaser, which is extremely useful when inspecting variables.

![ISA]({{ site.url }}/scrambledev/assets/images/screenshots/PART1.png)

The circle around the body displays the speed (magnitude of velocity) nicely. I have also added some custom lines using [Phaser Geometry](https://phaser.io/examples/v2/category/geometry) to display normal acceleration (green), lift force, drag force, because i'm pretty sure this will be useful later on. 

At this point I added basic keyboard cursor input just to goof around. The flight realism is nowhere to be found yet. Right  now you can freely move around, kind of like [this](//examples.phaser.io/embed.php?f=weapon/asteroids.js) example:

{% raw %}

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="800" height="600" src="//examples.phaser.io/embed.php?f=weapon/asteroids.js"></iframe>
{% endraw %}

#### All examples are embedded from the [Phaser examples](https://phaser.io/examples) (MIT License) and are not owned by me in any way.

*Scramble JS uses Phaser 2 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*