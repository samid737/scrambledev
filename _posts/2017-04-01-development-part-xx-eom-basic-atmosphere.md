---
title: 'Development part 2: modeling EOM'
layout: post
---

*Please not that these features where implemented in the early stage, prior to  logging the progress.  Not all details are included.*

Normally when working on A flight simulator, you consider motion in three dimensions. There are quite alot of resources and even [example projects](https://www.google.nl/search?q=flight+simulator+github) available that implement flight in three dimensions. However, these rely on A particular set of assumptions. The problem in my case is that my assumptions differ from the reference material. The good news however lies in the number two of 2D, I can bypass an entire dimension...

## Equations of motion (EOM)

There are A view fundemental equations I applied to determine the motion of the aircraft and the main source  is the [Flight and Orbital Mechanics](https://ocw.tudelft.nl/courses/flight-orbital-mechanics/) course I took, given  by Dr. ir. M. Voskuijl.

Basically this course deals with the mechanics involved during every phase of flight (take-off, climb, cruise, descent, landing) and the nice part is that complete derivations are  included for 2D longitudinal flight !

### Translation

For translational motion, the following equations are applied for 2D longitudinal flight:

{% raw %}
  $$\boldsymbol{ F_x= m a_x = T  \cos( \theta)-D \cos(\gamma)-L \sin(\gamma)}$$ \\
	$$\boldsymbol{ F_y= m a_y = T  \sin( \theta)-D \sin(\gamma)+L \cos(\gamma) -W}$$ \\
	\\
	where $$ \boldsymbol{\theta}$$ is the pitch angle, $$\boldsymbol{\gamma}$$ is the flight path angle, $$\boldsymbol{L}$$ the Lift force, $$\boldsymbol{D}$$ the drag force, $$\boldsymbol{T}$$ the total thrust and $$\boldsymbol{W}$$ is the weight of the aircraft (and $$\boldsymbol{m}$$ the mass, being $$\boldsymbol{\frac{W}{g}}$$).
 {% endraw %}

In most derivations, the flight path angle is approximated to be small, but this does not hold for this flight model ([Assumption](#)). The thrust force is therefore dependent on the pitch angle, not flight path angle. The force is  assumed to act along the body axis of the aircraft, so inclination angle of engines is  not considered  ([Assumption](#)).

#### Weight

The weight is initially given and will decrease troughout  flight (fuel burn).

#### Thrust

The thrust is also A variable during flight, but the maximum static thrust an engine can provide  is also A known value.

#### Lift

The lift force is basically determined by the shape of the wing, air density, the wing surface, the speed of the aircraft. 

{% raw %}

  $$\boldsymbol{ L = C_L \frac{1}{2} \rho v^2 S }$$  \\
	\\
	where $$ \boldsymbol{\rho}$$ is the air density, $$\boldsymbol{S}$$ is the wing surface area, $$\boldsymbol{v}$$ the speed of the aircraft, $$\boldsymbol{C_L}$$ the lift coefficient of the aircraft.
 {% endraw %}

The lift coefficient is A [linear function of the angle of attack](https://qph.ec.quoracdn.net/main-qimg-92f5bb8bbe8f7088e166a2fb64fbce41):

{% raw %}
  $$\boldsymbol{ C_L = \frac{dC_L}{d\alpha}(\alpha - a_{L=0})}$$  \\
	\\
	where $$ \boldsymbol{\frac{dC_L}{d\alpha}}$$ is the lift slope, $$\boldsymbol{\alpha}$$the angle of attack , $$\boldsymbol{a_{L=0}}$$ the zero lift angle of attack.
 {% endraw %}

The angle of attack is  the parameter that can be controlled by rotating the aircraft A wing surface area can be controlled using high lift devices, but A constant wing surface is assumed for this flight model ([Assumption](#)). The lift force is controlled by rotating/pitching the aircraft. In a three dimensional world, the lift force will vary along the spanwise direction of the wing. Since we are dealing with A two dimensional wing, we can neglect spanwise lift distribution ([Assumption](#)).

#### Drag

The Drag force is basically determined just like how the lift force is determined, but the Drag Coefficient is A function of the Lift Coefficient. 

{% raw %}
  $$\boldsymbol{L = C_D \frac{1}{2} \rho v^2 S}$$  \\
	\\
	where $$\boldsymbol{ \rho}$$ is the air density, $$\boldsymbol{S}$$ is the wing surface area, $$\boldsymbol{v}$$ the speed of the aircraft, $$\boldsymbol{C_D}$$ the Drag coefficient of the aircraft.
 {% endraw %}
 
The parabolic [drag polar](https://en.wikipedia.org/wiki/Drag_polar) is used to determine $$\boldsymbol{C_D}$$:

{% raw %}
$$\boldsymbol{C_D =C_{D0} + \frac{C_L^2}{\pi Ae}}$$
 {% endraw %}

where $$\boldsymbol{ C_{D0}}$$ is the parasitic drag coefficient, $$\boldsymbol{A}$$ is the aspect ratio of the wing, $$\boldsymbol{e}$$ the oswald/wing efficiency factor.

### Rotation

Notice that the the lift force and in turn the drag force can be influenced by controlling [the angle of attack](http://i43.tinypic.com/5n1yrc.jpg), which has the following relation:
 
{% raw %}
  $$\boldsymbol{\alpha =\theta - \gamma}$$
	 {% endraw %}

The pitch angle is controlled during flight by changing lift distribution at the tail of the aircraft, which results in torque being applied about some point in space  which rotates the entire body. Therefore, to completely describe the motion of the aircraft The following relation is used:

{% raw %} 
  $$\boldsymbol{\mu = \frac{d^2 \theta}{dt^2} = \frac{\tau}{I} }$$ \\
	\\
where $$\boldsymbol{ \mu}$$ is the angular acceleration, $$\boldsymbol{ \theta}$$, the rotation angle, $$\boldsymbol{ \tau}$$, the net torque applied, $$\boldsymbol{I}$$, the moment of inertia of the body.   
{% endraw %}

The equations shows that If the torque applied can be controlled, then the rotation/pitch angle of the aircraft can be controlled.

## Modeling EOM

### Translation
Notice the acceleration terms $$a_x$$ and $$a_y$$ are immediately found if all forces are known. A physics body in Phaser has an [acceleration](https://phaser.io/docs/2.6.2/Phaser.Physics.Arcade.Body.html#acceleration) property, so the challenge is to find these quantities, scale them by some factor (Phaser works with pixels instead of meters) and apply those values to the Arcade Physics system in order to translate the aircraft. 

### Rotation

Phaser also allows the user to set [angularAcceleration](https://phaser.io/docs/2.6.2/index#angularAcceleration) , which is precisely what we need in our case. The challenge is to find values for torque and moment of Inertia. The moment of Inertia can be easily calculated by assuming the aircraft to be of elliptical shape([Assumption]()). The torque that is applied varies with time and (luckily) we can find values for torque numerically. The centre of gravity of the rigidbody is assumed to be fixed along the longitudinal axis of the aircraft ([Assumption]()).