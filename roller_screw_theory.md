



# Inverted Planetary Roller Screw

A low friction mechanism that translates rotation into linear movement with high mechanical advantage

Roller screws are useful if you have a load-bearing linear actuator and want to push the frontier in one of:
- Faster speed
- Larger force
- Lower power


## Contents

  - [Terminology](#terminology)
  - [Name](#name)
  - [Function](#function)
  - [Mechanism tradeoffs](#mechanism-tradeoffs)
  - [Mechanical advantage](#mechanical-advantage)
  - [Function of a regular screw](#function-of-a-regular-screw)
  - [Benefit of an efficient screw (roller screw)](#benefit-of-an-efficient-screw-roller-screw)
  - [Roller screw parameters](#roller-screw-parameters)
  - [How parts rotate](#how-parts-rotate)
  - [Intuition for main action](#intuition-for-main-action)
  - [Threads](#threads)
  - [Planetary roller screw vs inverted planetary roller screw](#planetary-roller-screw-vs-inverted-planetary-roller-screw)
  - [Output force calculation](#output-force-calculation)
  - [Spur gear](#spur-gear)

## Terminology

- Thread start
    - A tooth that spirals around to form a thread. Two starts means
    that at the base there are two teeth that exist. The ridges on the
    thread will alternate, one from each tooth.
- Screw ("Sun")
    - The central core of the mechanism with a thread
- Rollers ("Planets")
    - Smaller cylinders that spin and revolve around the core
    - Have a thread with one start
- Nut ("Ring")
    - Outer cylinder with an internal thread
- Carrier
    - A disk that holds the planets in alignment
- Spur gear (cut on the rollers)
    - Ensures the rollers turn at the right rate
    - The spur gear is cut onto the roller thread so that the spur gear
    does not get in the way of the roller thread meshing with the nut thread.
- Spur gear (either on the screw or the nut)
    - Ensures that the rollers turn at the right rate


## Name

Inverted Planetary Roller Screw

- Inverted: The spur gear is not on the nut. It is on the inner screw.
- Planetary: The rollers orbit the central screw.
- Roller: The planets are elongated compared with a regular planetary gear.
- Screw: The main function of the device is to spiral forward, like a screw.

## Function

The assembled components all fit inside the nut. The assembly drives in and out
of the nut as some part is rotated. The rotated part is either the nut or the screw.

This effectively gives different modes of operation.
    - Turn the screw, hold the nut
        - A motor can drive the screw to convert rotation to linear actuation.
    - Turn the nut, hold the screw
        - The nut can be powered by elecromagnetism to form a compact linear actuator.

The main reason to use the roller screw is that it can turn even when under large loads.

## Mechanism tradeoffs

We trade off complexity to get an efficient mechanism that works under loads.

| Mechanism                    | Complexity                                                                                          | Friction Kind           | Tolerance to load                                                                                                               |
|------------------------------|----------------------------------------------------------------------------------------------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| A rack and pinion            | Good. The pinion spins and the rack moves in a line.                                               | Good (rolling)          | Bad. If one pushes on the pinion, the force is transmitted to oppose the rotation of the motor.                              |
| A rack and worm gear         | Good. The worm gear is rotated and spins against a rack. The rack moves in a line.                 | Bad (sliding)           | Good. If one pushes on the rack, the teeth on the gear transmits the force along the gear axis, rather than opposing rotation.   |
| A screw jack or vise         | Good. A screw turns within a nut, which advances the screw.                                        | Bad (sliding). Approximately 20% efficiency. The friction is sliding friction along the contact of the thread. | Good. If one pushes on the nut, the force is transmitted to the screw teeth, which does not oppose the motion.                |
| Inverted planetary roller screw | Bad. A screw turns and rotates threaded rollers inside a larger nut. The rollers together act as virtual screw within the nut which moves the screw into the nut. | Good (rolling). Approximately 80% efficiency. The screw rolls on the rollers and the rollers roll on the nut. It is technically sliding friction at each contact point of the rollers. Overall, the action is low friction rolling kind. | Good. If one pushes on the nut, the force is transmitted to the roller teeth then to the screw teeth, then to the axis of the motor, rather than opposing the rotation of the motor. |



## Mechanical advantage

When the screw is driven by an input torque, the output force is subject
to a multiplier as follows:
```
force_out = torque_in * 2 * pi / (num_starts * thread_pitch_meters)
```
The derivation of the equation is covered in a later section.

For example a thread with one start and a 6mm (0.006m) pitch would result in
a mechanical advantage of 1000x. A 10NM input torque could generate 10kN of force
in a frictionless environment.

## Function of a regular screw

Screws have tremendous ability to turn an input torque into a large force.
Consider a vise, which uses the lead screw to apply a large force.

To understand this, consider a perfectly efficient vise with a very long lead screw. With a lead of 6.3m (2 * pi), the screw has no mechanical advantage. An input of 10Nm torque would translate to an output force of 10N.

Yet, normal leads are about 1000 times shorter (6mm vs 6m) and the gain is therefore 1000x. So
10Nm input torque creates about 10KN output force. If a screw has terrible efficiency (10%), it can still create 1kN output force.

So, because the neutral lead (6.3m) is so large compared with leads practically used, it does not matter how inefficient a screw is normally. The result is usually "good enough".

## Benefit of an efficient screw (roller screw)

What if screws were 10x more efficient? That is the niche that roller screws fill. Practically, we are talking about clamping a piece of wood with a bench vise with a handle 10x shorter. What are areas where this is actually beneficial?

- Huge forces that stress mechanical parts, like in large industrical presses. A vise can only be used up to the point where the handle starts to bend. A low efficiency means that the handle will bend before higher forces can be delivered.
- Systems sensitive to total energy use. A low efficiency means that a low percentage of energy is being used for the task. So battery based systems (robotics, space industries).
- Systems designed for speed. A low efficiency means that the force being delivered has to be over a short distance (a small lead). An increase in efficiency means the lead can be longer. This means the output force can be delivered over longer distances. This is equivalent to having a vise move faster without sacrificing strength.

A roller screw is an efficient screw, roughly 80-90% vs 10-20% as seen in other
screw based devices (screw jack, vise). This makes them good for heavy industrial processes, robotics, aerospace and performance.

In summary, a the efficiency of a roller screw can be used to get one of:
- Larger output force
- Faster output speed
- Longer output duration

If an application is not already pushing the limits of a particular variable above, then a roller screw adds complexity without a material gain.

## Roller screw parameters

As a screw, the main parameter to control is the lead. For every turn of
the screw, how much does the assembly advance in the nut? A higher lead
gives faster speed but less strength.

The parameter selection is best done as follows:
- Choose the diameter of the nut based on how small the mechanism needs to be
- Choose the thread pitch based on how fine you can manufacture one
- Choose the number of thread starts based on how much gearing you need
- Choose if the device is a precise and low energy application or chunky and high energy (gear modulus)

All remaining parameters basically are derived from the above.

For example. Knowing the thread starts gives you the diameter of the rollers and screw.
That allows the spur gear diameters to be known. Given the approximate modulus,
this allows the spur gear teeth counts and profiles to be derived.

See the recipe page for a more thorough explanation.

## How parts rotate

In a regular planetary gearset, the carrier rotates according to the number
of teeth on the sun and ring gears. That is not the case for the roller screw.

The rollers instead move by rules more akin to how parts of a spirograph move.
The movement of the carrier is determined by the size of the rollers relative to
the screw. This has to do with the least common multiple of these numbers.

This is more academic (or for making perfect animations). Roller screws work by
advancing the assembly in the nut. The number of rotations of the carrier is not
required for gear calculations. In contrast, these numbers are important for regular planetary gearsets where the carrier may be the direct output.

There are two parts to how the assembly advances. Together the result is
the assemble advances one lead length (pitch * starts) per screw rotation.
- Carrier rotation
    - The rollers physically move
    - Related to the sizes of the spur gears (the radius of the screw/rollers)
- Roller rotation
    - The rollers turn
    - Related to the thread starts on the screw. With more starts the rollers turn more because they only have one thread start.



## Intuition for main action

To understand what happens in the roller screw, imagine the set of rollers as a single virtual screw
with the rollers fixed in place. Around the whole set, one can draw a virtual thread that wraps around
all the rollers. With this large virtual screw, one can imagine screwing it into the large nut housing. The rollers simply replicate the thread on the inner screw, but at a larger diameter and in a way that has better friction properties.
If the inner thread has multiple starts, so does the virtual thread.

One can indeed do this with the roller screw setup if is sloppy enough. The rollers can be held
to prevent them rolling and the whole set can be rotated to insert into the nut. However this is
bad because as they move in, the primary interaction is sliding friction. Sliding friction
requires a lot of force and has high energy loss to heat.

Instead, the rollers rotate and orbit around the screw. As each roller turns, its thread turns
and the outermost contact points on the roller shift. Together, the rollers orbit around the screw.
The effect of these two things combined is that a virtual screw is rotating. Imagine a screw whose
contact points keep being replaced by miniature rotation systems. Each roller is one such rotation
system.

In summary, a roller screw is a screw whose surface is a slippery and changing thing. That
is what makes it low friction.

## Threads

Two threaded rods can rotate against each other as helical gears. A thread may have a number of
starts. One start being a single tooth that winds all the way along. Two starts meaning that
every second ridge along the screw is the same tooth.

As the two threaded rods rotate against each other, the thread starts at the end of the rod must line
up to mesh. In this way, they are functionally equivalent to teeth. A rod with 4 starts that rotates
against a rod with 1 start is like a gear ratio of 4 to 1. For every rotation of the first rod, the
second rod rotates 4 times.


## Planetary roller screw vs inverted planetary roller screw

The inverted planetary roller screw (IPRS) has some differences to the regular planetary roller screw (PRS).

The central rod in an IPRS is only threaded for a short distance. This allows an extension rod to be used and for the nut to be sealed and lubricated. A PRS has a screw the entire length of the rod, and cannot be sealed as compactly.

In contrast, a PRS allows the nut to be a short length, rather than having it span the length of the linear travel of the mechanism.

## Output force calculation

For every rotation of the screw, it advances exactly one lead.

Hence for all IPRS driven like this, one rotation will cause linear movement of half the lead
```
linear = lead
```

Consider a rack and pinion. The stepper motor can be imagined as driving the pinion.
For one rotation the rack advances `linear` amount, which is equal to the circumference of the
pinion. The radius of the pinion is therefore:

```
cicumference_pinion = 2 * pi * r_pinion
r_pinion = cicumference_pinion / (2 * pi)
r_pinion = lead / (2 * pi)
```
The stepper is generating torque at that pinion radius. This causes the rack to advance with
a force:
```
torque_stepper = force_rack * radius_pinion
torque_stepper = force_rack * lead / (2 * pi)
force_rack = torque_stepper * 2 * pi / lead
```

If the output rack force is applied at 1m, that will be the output torque in Nm.

The gain calculated as:
```
gain = output / input
gain = force_rack / torque_stepper
gain = (torque_stepper * 2 * pi / lead) / torque_stepper
gain = 2 * pi / lead
```

Hence as the lead increases the torque gain decreases.

If the lead is 16mm, the gain is:
```
gain = 2 * pi / 0.016
gain = 392
```

So the only way to increase the gain is to reduce the lead, which can be achieved either
by reducing the starts and the pitch.
```
lead = num_starts * pitch
```

This demonstrates the fundemental tradeoff: spin the motor more revolutions for a given linear
travel to gain force.

So in the context of the roller screw, this would be:
```
force_out = torque_in * 2 * pi / lead
```
A cheap 0.3Nm stepper motor driving an inverted planetary roller screw with a 10mm (0.01) lead would produce a force of 188N, enough to drive a ~15kg platform updward.

## Spur gear

Roller screws have a spur gear cut into the thread of the rollers. This gives a mechanism to
ensure the rollers are synced with the screw, which prevents them migrating along their axes.
The gear is not a high energy gear, it is only used for timing.
