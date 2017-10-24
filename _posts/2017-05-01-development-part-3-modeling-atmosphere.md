---
title: 'Development part 3: Modeling atmosphere'
layout: post
---

*Please not that these features where implemented in the early stage, prior to  logging the progress.  Not all details are included.*

The accuracy of the flight model depends on the atmosphere model. The ISA standard atmosphere up to stratosphere altitude is modelled for best accuracy. The main references are found [here](http://www.wxaviation.com/ISAweb-2.pdf), and [here](https://www.grc.nasa.gov/www/k-12/airplane/atmosmet.html).  The temperature, air density and pressure is computed up to stratosphere altitude.

## Formulas
![ISA]({{ site.url }}/scrambledev/assets/images/ISA.png)

For altitudes up to 11km the following formulas are used:

{%raw%}
$$\boldsymbol{T= T_0 - 6.5 \frac{h}{1000}}$$\\
\\
$$\boldsymbol{P= P_0  (\frac{T}{T_0})^{5.2561}}$$\\
\\
where $$\boldsymbol{T}$$ is the Temperature at altitude $$\boldsymbol{h}$$, $$\boldsymbol{T_0}$$ A reference temperature (Sea level), $$\boldsymbol{P_0}$$ A reference pressure (Sea level).
{%endraw%}

    T = T0 - (6.5 * h / 1000);
    P = P0 * (Math.pow(T / T0, 5.2561));

For altitudes up to 20km, isothermal conditions exist and the pressure formula is slightly different. Then above 20km the same relation as above holds for $$\boldsymbol{P}$$ and $$\boldsymbol{T}$$, except for the increase in temperature.

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
where $$\boldsymbol{v}$$ is the speed of the aircraf, $$\boldsymbol{M}$$ the Mach number.
{%endraw%}

## Modeling

The formulas are directly applied and computed every 0.25 seconds to avoid unnecessary computation. I still have to consider  whether caching precomputed values is A better solution, but I will hold that thought for the optimization phase. Gravity is assumed to be constant with increase in altitude ([Assumption]()). World atmospheric conditions are yet to be implemented. Wind is yet to be implemented.