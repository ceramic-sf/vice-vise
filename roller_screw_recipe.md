## Recipe

Steps to follow to make an inverted planetary roller screw (IPRS).

For a working CAD model that uses this recipe, see the `model` directory.

  - [Recipe](#recipe)
    - [Main performance parameters](#main-performance-parameters)
    - [Thread tooth](#thread-tooth)
    - [Pitch](#pitch)
    - [Starts](#starts)
    - [Linear speed](#linear-speed)
    - [Mechanical advantage](#mechanical-advantage)
    - [Nut radius](#nut-radius)
    - [Roller diameter](#roller-diameter)
    - [Screw diameter](#screw-diameter)
    - [Screw thread length](#screw-thread-length)
    - [Spur gear length](#spur-gear-length)
    - [Roller length](#roller-length)
    - [Nut length](#nut-length)
    - [Screw surface radius](#screw-surface-radius)
    - [Roller surface radius](#roller-surface-radius)
    - [Nut inner surface radius](#nut-inner-surface-radius)
    - [Spur gear diameters](#spur-gear-diameters)
    - [Spur gear CAD](#spur-gear-cad)
    - [Spur gear teeth](#spur-gear-teeth)
    - [Roller thread](#roller-thread)
    - [Roller count](#roller-count)
    - [Carrier](#carrier)
    - [Circlip](#circlip)
    - [3D printing tips](#3d-printing-tips)
    - [Assembly tips](#assembly-tips)



### Main performance parameters

The screw may have a slow and strong thread, or a fast and weak thread. This
is controlled by two factors, the thread pitch and the thread starts.

|                | One Start | Few Starts | Many Starts | Comment       |
|----------------|----------|-----------|------------|----------------|
| Small Pitch    | Too slow | Great torque & precision  | Too sensitive to tolerances | Strong & slow, delicate thread |
| Medium Pitch   | Great torque & robust | **Choose this one** | Great speed & precision |                |
| Large Pitch    | Too weak central screw | Great speed & robust |   Too senstive to loads | Weak & fast, delicate roller carrier |
| Comment        | Slow & strong, big rollers |           | Fast & weak, small rollers |                |

Select an all rounder by default, something that you can make easily and use reliably and practically.

Screws work by dividng work done over a large distance. The lead of the screw (linear travel per rotation) determines exactly how much torque/precision/speed/robustness. Roller screws do the same but with low friction.

The roller screw gains the benefit of low friction by increased complexity compared to a regular screw. Attempts to optimise too hard (tiny lead, huge lead) can significantly impair an otherwise complex mechanism.

Screws already have a huge mechanical advantage. A frictionless screw that has a lead of 2 * pi (~6 meters) has no mechanical advantage. A 3 meter lead has 2x advantage, and a lead of 6 millimeters has 1000x advantage. Hence, it is the main
priority to get the mechanism produced and reliably operating rather than tweaking the lead to get slightly better mechanical advantage.


### Thread tooth

The teeth on all the threads (rollers, screw, nut) are the same.

The tooth is wrapped around a cylinder to make the thread. The base of the tooth is equal to the thread pitch. The height of the tooth depends angle in the apex of the tooth.

A triangle with 90 degrees at the apex is standard, but other profiles (60 degrees) may work.

Some sources recommend optimising the teeth of the roller thread by making them slightly convex to reduce friction. For a basic construction a simple straight edge may be used, which allows reuse of the tooth profile for the screw, roller and nut.

### Pitch

The distance between adjacent ridges of the thread. This will be the base of the tooth triangle.
As such, this also controls how tall the tooth is.

As pitch increases, the torque drops and speed increases.

A small pitch may be hard to manufacture. A large pitch may make the teeth too big to fit
in the roller screw.

### Starts

With the pitch selected the actual lead of the screw can now be decided. This is how much linear distance will be traveled per full rotation of the mechanism (either the nut or the screw).
```
lead = pitch * thread_starts
```

|      Lead          | 1 Start | 2 Starts | 3 Starts | 4 Starts |
|----------------|----------|-----------|---------|---------|
| 4mm Pitch    | 4mm     | 8mm      | 12mm    | 16mm    |
| 8mm Pitch    | 8mm     | 16mm     | 24mm    | 32mm    |
| 12mm Pitch   | 12mm    | 24mm     | 36mm    | 48mm    |

### Linear speed

If the roller screw is being driven by a motor, then the maximum rotation of the motor will determine the maximum linear speed of the final mechanism.
For a motor with a certain rotations per minute (RPM):

```
linear_speed_per_second = motor_rpm * lead / 60
```
This may help inform the selection of the pitch and thread starts.
However, speed is inversely related to mechanical advantage.

### Mechanical advantage

Now that the lead is known, the mechanical advantage can be calculated.

Consider a screw driven by 1 Nm of torque for a full rotation. The screw will
extert a constant linear force.
```
force_out = torque_in * 2 * pi / lead_meters
```

|Force out from 1 Nm input| 1 Start | 2 Starts | 3 Starts | 4 Starts |
|----------------|----------|-----------|---------|---------|
| 4mm Pitch    | 1570 N     | 785 N      | 523 N    | 392 N    |
| 8mm Pitch    | 785 N     | 392 N     | 261 N    | 196 N    |
| 12mm Pitch   | 523 N    | 261 N     | 174 N    | 130 N    |

So the bottom right configuration may have 12x faster linear travel, but 12x less force during that distance.

As an example, a cheap NEMA17 stepper motor such as those found on basic 3D printers may have 0.3Nm of torque. That motor could power the roller screw to lift a platform upward. The maximum amount of weight it could lift would be as follows. Note that twice the lift means half the speed.

| Lifting capacity of 0.3 Nm motor | 1 Start | 2 Starts | 3 Starts | 4 Starts |
|---------------------------|---------|----------|----------|----------|
| 4mm Pitch                 | 47 kg   | 24 kg    | 16 kg    | 12 kg    |
| 8mm Pitch                 | 24 kg   | 12 kg    | 7.8 kg   | 5.9 kg   |
| 12mm Pitch                | 16 kg   | 7.8 kg   | 5.2 kg   | 3.9 kg   |

This ignores friction, which for roller screws would result in ~10-20% loss.


### Nut radius

How wide can you make the cylinder of the roller screw? Where will it be used? Pick the largest you can tolerate,
as this gives the most choice in performance for other parameters.
If the nut is very large, rollers that are a small fraction of the nut size may be easier to manufacture.
```
radius_nut
```

### Roller diameter

Now that starts are known the roller size can be calculated as follows:
```
radius_roller = radius_nut / (num_starts + 2)
```

As the nut contains the screw and the rollers, their radii follow (nut must fit 2 rollers and one screw across the diameter).

The rollers always have one thread start. As the number of thread starts increases, the rollers complete more turns per revolution of the nut or screw.
As they rotate faster, they must be smaller in order to complete full turns.


|| 1 Start | 2 Starts | 3 Starts | 4 Starts | 5 Starts |
|----------------|----------|-----------|---------|---------|---------|
|  `radius_roller`  | `r_nut / 3`    | `r_nut / 4`  | `r_nut / 5`| `r_nut / 6` |`r_nut / 7`|


### Screw diameter


```
radius_screw = radius_nut * (num_starts / (num_starts + 2))
```

|| 1 Start | 2 Starts | 3 Starts | 4 Starts | 5 Starts |
|----------------|----------|-----------|---------|---------|---------|
|  radius_screw  | `r_nut / 3`| `r_nut / 2`| `r_nut * 3 / 5`| `r_nut * 2 / 3`|`nut * 5 / 7`|


### Screw thread length

Teeth on the rollers engage in the screw and nut and distribute load. The
longer the screw, the less load on each tooth.

A longer screw also increases the stability of the mechanism. Too long, and it will take up linear space and lose some efficiency.


### Spur gear length

Before and after the screw thread, there is a spur gear on the screw. This engages
with the roller and ensures they move correctly.

The spur gear on the planets is cut axially onto the ends of each roller. The
axial length of the spur gear should be at least a few multiples of the pitch, so that the spur gear teeth are always engaged with the planet teeth.
```
spur_gear_length >= 3 * pitch
```

### Roller length

The rollers must be long enough to engage with the screw thread and the two screw spur gears.
```
roller_length = screw_thread_length + 2 * spur_gear_length
```
### Nut length

Determines how far the mechanism can travel. Flexible, but at least as long as the planets. When the same length, the roller screw leaves the nut, which means fewer teeth engaged for strength and stability.

```
nut_length >= roller_length
```

Optimally, screw is extended by a rod so that the mechanism is always inside the nut. This would also enable the mechanism to be sealed and lubricated. If the rod was equal to the roller lenght, and the nut twice the roller length, then the mechanism could safely travel linearly a distance equal to the roller length.

### Screw surface radius

The calculations of the perfect radii of the nut, screw and rollers above is
for the pitch line. This is the line where two cylinders meet perfectly and
have identical surface velocities at this point.

In reality the the surfaces have teeth, which are sometimes above and sometimes below this line. There will be some minor friction as the teeth mesh imperfectly. The tooth should be half above and half below this line.

To create the thread, create a cylinder, place the tooth and do a helical pad.
The helix should travel one lead per revolution. Use a polar pattern for the number of thread starts.

The radius of the screw and roller cylinders will be their pitch radius minus half the tooth height. For the nut, the pitch radius plus half the tooth height.
For a 45 degree tooth this will be `(pitch / 2) / 2`.

```
screw_body_radius = screw_ideal_radius - thread_pitch / 4
```
### Roller surface radius

Similar to the screw, the roller surface on which the thread is added is:

```
roller_body_radius = roller_ideal_radius - thread_pitch / 4
```

The roller body radius is important because this engages with the carrier, and will be weak if too small. One can see that if the thread pitch cannot be larger than `4 * roller_ideal_radius`.


### Nut inner surface radius

As a cylinder, the thread is applied to the inner surface of the nut, and so the
radius will be larger than the pitch line.

```
nut_body_radius = nut_ideal_radius + thread_pitch / 4
```

One can see that once the structural component of the nut is added, the widest point of the roller screw assembly will be `nut_body_radius + nut_wall_thickness`

### Spur gear diameters

The spur gear will have the same pitch line as the main screw pitch line.
Its purpose is to make sure each roller does not over or under rotate, which would cause axial migration.

```
screw_spur_pitch_radius = screw_ideal_radius
```
The screw spur gear will mesh with a spur gear that is cut onto the end of the roller (like a cookie cutter pushed onto the end).
```
roller_spur_pitch_radius = roller_ideal_radius
```

### Spur gear CAD

To create the gear in CAD, use a involute gear design with the module and tooth count. For the screw, pad the
gear shape. For the roller, pad the gear, then create a cylinder and then XOR to create a
cookie-cutter with a spur gear shaped hole. Place one on each end of the roller and use the cut tool
to cut the thread.

### Spur gear teeth

Two spur gears will mesh if they have the same module.
```
module = pitch_diameter / tooth_count
```

One way to think of the module is as a proxy for the energy involved.

| **Module (mm)** | **Purpose**                                |
|-----------------|--------------------------------------------|
| 0.1 - 0.5       | Ultra-fine precision                       |
| 0.5 - 1.0       | Compact, precise mechanisms                |
| 1.0 - 2.0       | General purpose precision                  |
| 2.0 - 4.0       | Moderate load systems                      |
| 4.0 - 6.0       | Higher load-bearing machinery              |
| 6.0 - 10.0      | Large-scale, high-load systems             |
| 10.0+           | Very large            |

Experimentally, a module of about 1.25 works well.

First work out exactly what module will give a whole number of teeth:

```
tooth_count ~= pitch_diameter / approx_module
```
Using a floor calculation allows this to be automated.
```
screw_spur_tooth_count = floor(screw_pitch_diameter / 1.25)
```

Actual module:
```
actual_module = screw_pitch_diameter / screw_spur_tooth_count
```
Then find the roller tooth count
```
roller_spur_tooth_count = roller_pitch_diameter / actual_module
```

### Roller thread

The rollers only one thread start, even when the screw and nut have more.
This means that the lead of a roller itself will be the same as the pitch.

Additionally, the roller thread is the opposite direction of the screw and nut threads. That is, a roller screw with a right hand thread will have right hand nut and screw, but left hand rollers. Turning such a screw in a clockwise direction would advance the screw and roller assembly forward into the nut.

### Roller count

The number of rolllers is flexible and one gains strength and stability
by adding more. More rollers can fit with more screw thread starts a smaller
pitch.

### Carrier

The ends of the rollers must have a portion without a thread. These fit into
a carrier, whose role is make it easy to align the rollers during assembly
and to prevent misalignment during operation.

The carrier need only be thick enough to be robust. It spins passively and
does not transmit load like in traditional planetary gearsets.

### Circlip

A clip placed on the screw to keep the carrier in place. A groove is placed on the screw to keep the circlip from moving axially.


### 3D printing tips

Some tips:
- Print rollers separately and with a raft as they may fall over during printing
- Print all threads vertically (standing up) so their surfaces are smooth when rotating


### Assembly tips

- Place rollers in hand, then the screw on top, then wrap two rubber bands around to keep them
all together.
- Move the rollers around under the rubber bands until they are evenly spaced.
- For each roller rotate in place until it is symmetrical relative to the spur gears. Rotation
to the next spur gear tooth will cause the roller to migrate along its axis.
- Add both carriers and circlips, hold the planets and turn the screw.
If there is clicking, find which roller is
responsible and whether it is a print artefact or alignment problem. If needed,
remove one carrier and rotate the rod one spur tooth and try again.
