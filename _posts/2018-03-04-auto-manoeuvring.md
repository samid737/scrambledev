---
title: Auto manoeuvring
layout: post
---

This log will be brief in demonstration, tightly packed with explanation,  so [fasten your seatbelts](https://www.youtube.com/watch?v=Y9WDcPwAQ0g)!

*All updates are found in the [changelog](/scrambledev/2017/10/01/changelog.html).*

# Auto manoeuvring

Let's start with the demonstration first in order to figure out how it works:

## Mission

Auto manoeuvring is demonstrated.

### Briefing

Initial altitude 7.000ft, speed 600KTS.  The Auto manoeuvre system is enabled. You are **NOT** flying the plane.

### Flight

<iframe width="560" height="315" src="https://www.youtube.com/embed/A46othGUIkM?rel=0" frameborder="0" gesture="media" allowfullscreen></iframe>

Note that the aircraft is almost in complete autonomous flight! Also notice the green paths showing up incidentally (actually just me clicking the generateFlightPath button) during flight and notice how the aircraft is trying to follow these paths. 

## Path generation

Phaser 3 is armed with some  nice tools  to implement [path](https://labs.phaser.io/index.html?dir=paths/curves/) generation and these paths are actually [Bezier Curves](https://javascript.info/bezier-curve), which prove to be extremely useful, because we can generate any path we want with them.

By forcing the aircraft to follow this path, we can facilitate auto flight.

## Utilizing autopilot

The [previous log](/scrambledev/2018/01/08/phaser-3-port-cameras-reinforcement-learning.html) demonstrated the attempt of implementing AI using reinforcement learning, which was super interesting , but experimental. I am still convinced that this approach can provide results, but I had to proceed with an alternative and decided not to reside to this method for now, but instead further utilize the existing autopilot control system. 

The autopilot control system currently implements an all purpose [PID controller](https://www.npmjs.com/package/node-pid-controller), so I put my focus on utilizing the PID. 

The altitude controller keeps the aircraft steady at some height and controls the $$\boldsymbol{y}$$ of the aircraft. If you rethink this in terms of Bezier curves, then the altitude controller forces the aircraft follow a horizontal line, which is Aa bezier curve with control points:

$$\boldsymbol{P_0 = (x_0, y_0), P_1 = (x_1, y_0), P_2 = (x_1, y_0),P_3= (x_3, y_0)}$$

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAUAAAAFACAYAAADNkKWqAAAcVUlEQVR4Xu2de4xc9XmGvzOzu7ZrbG6BBBdKSwt0/6AqMqXlokIgoqlUxVFFMHdQVZaUqghKi7hI2C5SKkEDKpBLN9AKVFBoK2FVIC6VKDjQkGZNQDRdjELENVRcBDG3eHfmnOp3ZnbxeNfeF3tI/HvnGWk99sw7s/O95zzPnnNm9rioqqoKLrF27dpYt25d3cSaNWvqfw/yZePGjfX4K1euHOQaZmenj97VwKWPAgF2FiwC9FzB+2VvF+Dpo7cBBNjtAwEiwB3JAQF6rh8IEAHOyz3AewLPFiBbgPOuA2wBAjxbgLoeXX5AsgXIFiBbgAL3LsALo0oRlz4QIAJEgALyLsALo0oRlz4QIAJEgALyLsALo0oRlz4QIAJEgALyLsALo0oRlz4QIAJEgALyLsALo0oRlz6KiYkJfhMkIsbHx+uvdBkbG6u/BvkyOTlZjz86OjrINczOTh+9q4FLHwiwu1wRoOcK3i97uwBPH70NsAvMLjC7wIIVXHb5hFGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfCBABIkABeRfghVGliEsfxcTERCVNbB4aHx+P9JUuY2Nj9dcgXyYnJ+vxR0dHB7mG2dnpo3c1cOkDAXaXKwL0XMH7ZW8X4OmjtwF2gdkFZhdYsILLLp8wqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArwwqhRx6QMBIkAEKCDvArww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)

The altitude controller , controls the error:

$$\boldsymbol{e_{alt} = y_{reference} - y_{actual} } $$

By adjusting to a controller that not only considers $$\boldsymbol{y}$$, but also $$\boldsymbol{x}$$ as input, we can control the aircraft based upon distance checking:


$$\boldsymbol{e_{automan} = \sqrt{(y_{reference}- y_{actual} )^2 +(x_{reference}- x_{actual} )^2} }$$

Pictorially and going back to paths:

![BZR]({{ site.url }}/scrambledev/assets/images/BZR.png)

This shows that the distance between any point normal to the aircraft that intersects a path determines the error (notice yellow normal line in video).  The intersection point can be retrieved via [Bezier - Line intersection](https://pomax.github.io/bezierjs/) test.

## What's next

The final step is to add some sort of descision making logic to the auto manoeuvring system.  Completing this allows me to focus on less aircraft related stuff. I have already been working on some vehicle designs for ground objects(targets), the spritesheets still have to be assembled. A Vehicle class is already prepared and will need further implementation once vehicles will be added to the simulation.


*Scramble JS uses Phaser 3 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*