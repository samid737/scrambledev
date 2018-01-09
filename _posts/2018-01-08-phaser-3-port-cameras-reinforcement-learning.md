---
title: Phaser 3, Cameras, Reinforcement learning
layout: post
---

First off: Happy new year folks!  The holidays kept me away from my PC, but not for too long. Last month I decided to make A switch to [Phaser 3](https://phaser.io/phaser3), which is very close to being released. 
One of my favorite features includes the new Camera system. I am still doing research in implementing AI for other aircraft and Reinforcement learning is one of the approaches I  considered and experimented with during the holidays. 
Extremely fun, but difficult to harness.

Also note that I've recently added A subscribe form  at the bottom of the log, so for those of you who wish to receive these dev logs regularly via e-mail, please don't forget to subscribe! 

*All updates are found in the [changelog](/scrambledev/2017/10/01/changelog.html).*

## Phaser 3

As A close follower  and admirer of Phaser development, I regularly read trough the [dev logs](https://phaser.io/phaser3/devlog) of Phaser 3. Phaser 3 is currently approaching its first release and beta releases have been available for quite A while. I was hesitant on whether I should stick to Phaser 2 or move the codebase to Phaser 3. Phaser 2 by itself was A great platform to work with, but I was eager to explore new features of Phaser 3 and I just could not ignore the published beta releases. Of the many awesome new features, some I could really use:

- A new camera system
- A brand new rendering engine.
- New Sound features, including pitch tuning.
-  Lighting support.

The shift towards Phaser 3 is also A learning step to familiarize with the new API. So in the end it was A well made descision.

## Cameras

The new Camera system adds A whole new level of sophistication to the game. As I might have mentioned earlier, there is A simulated world, which is currently bounded in width and height, but I am still considering removing the horizontal bound (to bound or not to bound).
The world can now be explored via mouse movement while holding the R key,  which tells the camera to detach from its main target. 

With the addition of multi-camera support, I can consider adding minimaps and target/objective displays, object tracking with [lerp](https://en.wikipedia.org/wiki/Linear_interpolation) motion etc.

## Reinforcement learning

This was another experiment that kept me busy and probably even distracted from the main work needed to be done. [Reinforcement learning](https://en.wikipedia.org/wiki/Reinforcement_learning) is one way to implement an AI, but definitely not the easy way. I came up with the idea after finding out about [reinforcement learning being applied to the flappy bird game](https://github.com/yenchenlin/DeepLearningFlappyBird). In my attempts, I took the very first JS library I could find, [Reinforce JS](https://github.com/karpathy/reinforcejs), analysed the examples and tried to fit them to the aircraft by setting up A simple training objective. The objective was to fly in formation  by maintaining horizontal speed. The autopilot was set to the proper altitude, so the agent (the AI) could only act by adjusting throttle:

## Mission

Progress is demonstrated.

### Briefing

Initial altitude 40.000ft, speed 500KTS. The flight leader is flying with you, so try to keep up with your leader.The autopilot is set to ALT.

### Flight

<iframe width="560" height="315" src="https://www.youtube.com/embed/Ao0Ym0OZYvQ?rel=0" frameborder="0" gesture="media" allowfullscreen></iframe>

A day night cycle/ sky is added , high altitude contrails and smoke trails, which still need some tweaking and sonic boom. The camera can look freely using the mouse pointer while holding the R key. Also notice how the HUD tilts at the very end of the video, simulating pilot pilot head movement due to exposed g-forces.  

You can also see the RL agent in action. The agent observes the environment (leader position, my position, my speed , leader speed), takes some, possibly random , predefined actions (throttle up, throttle down, speed brake full, do nothing) and based upon some pre-defined reward scheme (your too far behind/past the leader, reward = -distance), it should learn to take the actions that minimizes the reward (if im next to the leader, reward = 0,  hmmm this looks,nice, try to keep on doing these kind of actions).

In my attempt, there where all sorts of problems I was faced with: Validating if it does learn and if it learns to converge to the right solution, the training time required,  the dimension of my state space and  the highly non-linear environment. In some test runs the agent was able to maintain perfect formation for about 10 seconds, but afterwards it would diverge. Yet I still believe with A bit more research it should be possible to get some sensible result, but darn you time....

With these features added I can work on scenery, for example some enemy ground objects, Runways to take-off and land from, buildings and A background environment. Weapon systems, combat flight, mission building would follow afterwards. The UI will be considered in the final stages. The main challenge is automating the generation of the scenery/world. It might  be necessary to implement A mission/scenery editor to facilitate the above. If you are interested in collaborating in the development, please feel free to contact me. I could definitely use some extra hands to work on these features.

*Scramble JS uses Phaser 3 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*