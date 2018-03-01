# scrambledev
Scramble development log. for more details please visit the [dev log](https://samid737.github.io/scrambledev)

Changelog:

## TODO:

- stall1 repeat bug.
- restructure namespace & JSON data to match systems. (engines, wings).

- meteorology:
- wind/turbulence.
- percipitation: rain, snow, dust.
- visibility.

- auto pilot altitude controller gain tuning, integral gain weak.
- %Speedbrake stuck after crash.
- World building.
- performance optimization.
- refactor constants.
- alt shift F.
- List of assumptions.


# 28-02-2017

## Features:

- Bezier based auto-manouvre prototype.
- Variable autopilot gains.

# 27-02-2017

## Features:

- Phaser 3.1.2 update.
- Added world element class.


## Bug fixes:

- Camera look zoomIn bug

# 23-02-2017

## Features:

- Added vehicle sprites (tank, rocket launcher, scud launcher).

# 08-01-2017

## Features:

- Phaser b15 update.
- Added Camera look.
- Added high altitude Contrails.
- closure/ Scramble namespace.

## Bug fixes:

- 

# 07-01-2017

## Features:

- Added Camera layering, camera class

## Bug fixes:

- HUD ladder mask WEBGL.
- World background not scrolling
- shock wave repeat.

# 06-01-2017

## Features:

- Added contrails, shock waves, clouds
- Added FX class.
- Day night cycle.
- Camera zoom buttons x,z
- Player class.
- Atmosphere class.

## Bug fixes:

-

# 27-12-2017

## Features:

- RL agent formation flight training.

## Bug fixes:

-Autothrottle NaN fix.
-Camera follow.


# 20-12-2017

## Features:

- Phaser 3 port 85%.
- RL agent.

## Bug fixes:

-Autothrottle NaN fix.
-Camera follow.

# 08-12-2017

## Features:

- Phaser 3 port 80%.
- Engine sound pitch.
- LG locked indicator.

## Bug fixes:


# 06-12-2017

## Features:

- Phaser 3 port 70%
- Camera logic improved.

## Bug fixes:


# 04-12-2017

## Features:

- Phaser 3 port 10%

## Bug fixes:


# 01-12-2017

## Features:

- Phaser 3 port 1%.

## Bug fixes:


# 23-11-2017

## Features:

- Pilot class
- HUD class.

## Bug fixes:


# 21-11-2017

## Features:

- Camera target switching.
- trim tabs, multiple control surfaces.

## Bug fixes:


# 20-11-2017

## Features:

- restructure code, engines
- autothrottle gain corrections.

## Bug fixes:

- fix aerodynamics
# 18-11-2017

## Features:

- add ground friction force.
- restructure aircraft components oop.
- JSON format aircraft data.

## Bug fixes:

- %landing rolling bug

# 17-11-2017

## Features:

- add ground friction force.
- restructure aircraft components oop.
- JSON format aircraft data.

## Bug fixes:

- %landing rolling bug

# 16-11-2017

## Features:

- JSON format aircraft data.

## Bug fixes:

- inertia incorrect

# 15-11-2017

- Moving scenery (relative positioning/reference frame).
- TAS correction.

## Features:

- structural damage indicator
- full power thrust sound
- idle thrust sound.
- recalibrate thrust/drag model, compressibility.

## Bug fixes:

- %reversed flight bug.
- %Display reset UR corner
- %display not resetting R

# 12-11-2017

## Features:

- structural damage indicator
- full power thrust sound
- idle thrust sound.
- recalibrate thrust/drag model, compressibility.

## Bug fixes:

# 26-10-2017

## Features:

- added cg debugging
- compressibility effect added using compressible Bernoulli equation.
- delta wing lift & drag model using Polhamus equation (low speed).

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
- Autothrottle

## Bug fixes:

- Correct fuel burn.
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