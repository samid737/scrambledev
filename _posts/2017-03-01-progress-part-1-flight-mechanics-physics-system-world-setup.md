---
title: 'Development part 1: Basic setup,sprite, physics system, world.'
layout: post
---

*Please not that these features where implemented in an early stage, prior to  logging the progress.  Not all details are included.*

## Sprite building

Once the [overall aircraft design ](/scrambledev/2017/01/16/aircraft-design-part-1.html) is complete, the MIG21 is split up into components and  A spritesheet is made using [TexturePacker](https://www.codeandweb.com/texturepacker). Phaser allows for hierarcichal setup of sprites. The parent sprite is the main body/fuselage, while other components (landing gear, elevators etc.) are set as [child sprites](https://phaser.io/examples/v2/sprites/child-sprites).

## Physics system
At this point, there is no physics involved,  just A sprite placed somewhere inside the game world. By using Phaser its [arcade physics](https://phaser.io/examples/v2/category/arcade-physics) system, we can begin giving some physical sense to the aircraft sprite (inside Phaser). The aircraft is considered to be A single rigidbody ([Assumption](#)).  Arcade physics is perfectly suitable for rigidbody dynamics and we can rotate and translate the aircraft using the following physics properties:

*  acceleration.
*  velocity.
*  position.
*  angularAcceleration.
*  angularVelocity.
*  rotation.

Arcade Physics collision detection is based upon Axis aligned boundary box (AABB) collision detection. For this game, collision detection is required for the following scenarios:

* ground impact.
* bullets/missile impact
* mid air collision.

Arcade Physics collision detection is therefore sufficient. The more advanced [P2 Physics system](https://phaser.io/examples/v2/category/p2-physics) will not be necessary.

## World setup

Scramble JS will be in 2D side view , hence the world is 2D, similar to UN Squadron for the SNES **(CLICK IMAGE FOR VIDEO)**:

[![CLICK FOR VIDEO]({{ site.url }}/scrambledev/assets/images/UN.png)](https://www.youtube.com/watch?v=-C6V_bEmOEQ&t=608s)

The frame of refence is pretty tricky to implement. In UN Squadron, the player can move around, but is bounded by the viewport and all objects are moving towards the player. This works fine for arcade/action gameplay, but for a simulated flight, it will make less sense. The game world is simulated using real world dimensions (everything is in SI units) and the level of action is not like in UN Squadron. 

The player can move around freely inside a simulated 2D world. In Phaser, you can set the size of your game world using A function called setBounds(). You can also let the main camera follow the player. The main camera follows the player only when it is in the vicinity of any scenery object. When there is no action, it will not follow the player, but the world position of the aircraft is still tracked. To illustrate:

TODO

A simulated world is setup by adjusting the world size to some  large (but not infinite) size. Since combat aircraft fly below the  [stratosphere](http://www.online-sciences.com/wp-content/uploads/2014/09/stratosphere-layer-11.jpg),  the height of the world will be less than the height of the stratosphere [ Assumption](#). I still have to think about A solution for the width of the world. It may be fixed, but could also vary with each mission.

*Scramble JS uses Phaser 2 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*