---
title: 'Modeling part 4: Atmosphere'
layout: post
---

*Please not that these features where implemented in the early stage, prior to  logging the progress.*

Currently, the aircraft can reach unrealistic altitudes (up to 180.000ft) due to innacurate thrust vs drag ratios at high altitudes. The current atmosphere is modeled as A linearly decreasing model, which is not true in reality. The [International Standard Atmosphere(ISA)](https://en.wikipedia.org/wiki/International_Standard_Atmosphere) up to stratosphere altitude is modelled for better accuracy. For now it is assumed that air is incompressible ([Assumption]()), but in reality this is not true for high speed flight (M>0.3). The main references are found [here](http://www.wxaviation.com/ISAweb-2.pdf),  [here](https://www.grc.nasa.gov/www/k-12/airplane/atmosmet.html), [here](http://s6.aeromech.usyd.edu.au/aerodynamics/index.php/sample-page/properties-of-the-atmosphere/variation-with-altitude/) and [here](http://nptel.ac.in/courses/112103021/module2/lec6/1.html).  The temperature, air density and pressure is computed up to stratosphere altitude.

![ISA]({{ site.url }}/scrambledev/assets/images/ISA.png)

## Analysis

For altitudes up to 11km the following formulas are used:

{%raw%}
$$\boldsymbol{T= T_0 - 6.5 \frac{h}{1000}}$$\\
\\
$$\boldsymbol{P= P_0  (\frac{T}{T_0})^{5.2561}}$$\\
\\
where $$\boldsymbol{T}$$ is the Temperature $$\boldsymbol{P}$$ the pressure at altitude $$\boldsymbol{h}$$, $$\boldsymbol{T_0}$$ A reference temperature (Sea level), $$\boldsymbol{P_0}$$ A reference pressure (Sea level).
{%endraw%}

For altitudes up to 20km, isothermal conditions exist and the pressure formula is slightly different. Then above 20km the same relation as above holds for $$\boldsymbol{P}$$ and $$\boldsymbol{T}$$, except this time there is an increase in temperature.

The air density can be determined from the ideal gas law:

{%raw%}
$$\boldsymbol{\rho = \frac{P}{RT}}$$\\
\\
where $$\boldsymbol{\rho}$$ is the air density at altitude $$\boldsymbol{h}$$, $$\boldsymbol{R}$$ the gas constant for air.
{%endraw%}

The Mach number determined as:

{%raw%}
$$\boldsymbol{M = \frac{v}{20.05 \sqrt{T}}}$$\\
\\
where $$\boldsymbol{v}$$ is the true airspeed of the aircraft, $$\boldsymbol{M}$$ the Mach number.
{%endraw%}

## Modeling

The formulas are directly applied and computed every 0.25 seconds to avoid unnecessary computation. I still have to consider  whether caching precomputed values is A better solution, but I will hold that thought for the optimization phase. Gravity is assumed to be constant with increase in altitude ([Assumption]()). 

## Result

Thrust, lift and drag forces are much more accurate. You can really notice thrust loss at high altitudes. The aircraft ceiling is definitely observable as it is almost impossible to reach altitudes above 70.000ft. The MIG-21 its ceiling is close to 60.000ft. Stall characteristics also seem to have improved.

## What's next

local atmospheric conditions are yet to be implemented. Wind is yet to be implemented. Weather is yet to be implemented.

*Scramble JS uses Phaser 2 as game engine. Fore more info, visit [Phaser.io](http://www.phaser.io).*