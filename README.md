# scrambledev
Scramble development log. for more details please visit the [dev log](https://samid737.github.io/scrambledev)

Changelog:

# TODO:

- add ground friction force.
- improve thrust/drag model, compressibility.
- pitch limiter controller gain tuning.
- auto pilot controller gain tuning, integral gain weak.
- %reversed flight bug.
- %landing rolling bug
- %Speedbrake stuck after crash
- %Display reset UR corner
- %display not resetting R
- IAS,TAS,EAS

- Moving scenery (relative positioning/reference frame).
- World building.

- Weather, snow, rain, heat/desert.
- Day night cycle.
- performance optimization
- refactor constants
- List of assumptions

# 26-10-2017

## Features:

- added cg debugging
- compressibility effect added using compressible Bernoulli equation.
- delta wing lift & drag model using Polhamus equation (low speed).
- idle thrust sound.

## Bug fixes:

- stability derivatives values, CG locations corrected.

# 20-10-2017

## Features:

- improved thrust model. velocity and altitude.
- supersonic drag polar

## Bug fixes:

- world scale (x vs y disproportional).

# 19-10-2017

## Features:

- pitch limiter.
- engine sound effects
- Autothrottle

## Bug fixes:

- Mach 2 check.
- Correct fuel burn
- Stall behaviour, vstall.

# 18-10-2017

## Features:

- Control damping, improve flight model.
- Autothrottle

## Bug fixes:

- positive feedback mach speed


# 17-10-2017

## Features:

- Autothrottle system.
- Autpilot alt_hold

## Bug fixes:

- plus minus signs altitude

# 11-10-2017

## Features:

- Atmosphere: Wind, Mach, improve rho.


## Bug fixes:

- HUD 360 degree BUG
- redout blackout invert
- calibrate altitude during TO/LND.
- TO/LND phase bug
- Flap reverse direction reversed.

# 8-10-2017

## Features:

- HUD: throttle, pitch, altitude, attitude, speed.
- tween the direction reversal.

## Bug fixes:

-

# 7-10-2017

# Features:

- added high lift device, flaps with two settings.
- added wing moment and tail moment debugging.
- added distance traveled parameter.
- added commanded and actual throttle input.

## Bug fixes:

- Air brake drag coefficient effect.

# 6-10-2017:


## Features:

- added weight parameters, operating limit parameters.
- added load factor parameter
- added Fuel burn parameter.
- added blackout,redout above 4G consistent Gload.

## Bug fixes:

- Take-off bug.

# 4-10-2017:

## Features:

- added afterburner mode, XXXXX N extra force above 95% throttle.

## Bug fixes:

- EOM, flight mechanics stable.
-
