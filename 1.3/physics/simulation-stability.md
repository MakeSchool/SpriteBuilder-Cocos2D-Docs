# Simulation Stability

You may find that physics glitches occur in your app. Some of these glitches are avoidable, others can only be reduced.

## Joints are "Soft" Constraints

All physics joints have some "softness" to them. If you need precise offsets / angle limits all the time, you can not rely on joints doing that for you at all times under all circumstances. Joints will allow physics bodies to move beyond the joint limits if only for a short period of time.

It is often trying to prevent these "softnesses" that cause physics glitches in the first place, either by applying too much force or manually intervening through code. 

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
The fact that, for example, a distance joint set to 30 points distance gives no guarantee that two bodies will be at a distance of **precisely** 30 points at all times is something to account for when designing your app.
</td></tr></table>

## Joints Add Forces to the Simulation

Connecting bodies via joints effectively adds continuous forces to the connected bodies and any bodies colliding with them. This can lead to instability (glitches) in the simulation, typically resulting in one of these behaviors:

- bodies never coming to rest (jittering)
- continuously generating collision events
- bodies getting stuck within each other
- bodies passing through (static) collisions
- bodies breaking their joint restraints (ie bodies folding in on themselves or overlapping)
- joints "exploding" (extreme forces cause bodies to move very quickly, very far apart)
- in the extreme case: crashes due to floating point values reaching infinity (NaN), typically as a direct result of a joint "exploding"

### Causes

Common causes for instability are:

- Joint constraints that are (near) impossible to resolve.
	- Example: two static bodies with a distance joint to the same dynamic body, whose allowed distances don't overlap so the dynamic body is continuously pulled towards one, then the other static body.
	- Example: a distance and a spring joint connecting the same two bodies, where the allowed distances prevent both joints from ultimately coming to rest while stiffness of the spring joint is high.
- Jointed bodies separated by a static body. This is like driving a wedge (static body) between two jointed dynamic bodies, which subsequently can no longer resolve their joint constraint. One of the dynamic bodies may even pass through collision.
- Jointed bodies stuck in other jointed bodies. The compound energy of one set of bodies trying to resolve their constraint will cause the other set of bodies to pull back trying to resolve their constraint.
- Manually moving/rotating bodies or constantly or unnecessarily applying forces/impulses. In particular when moving/rotating dynamic bodies via move/rotate actions. Games may have to manually modify the physics world to create the desired behavior in the first place. However one must be very careful doing so as these manual interventions may cause chain reactions where the physics simulation tries to resolve a forced-upon situation which manual processing code once again tries to resolve, repeat ad infinitum.


### Preventing Joint Instabilities

Besides the obvious, and ignoring the fact that in a decently complex physics simulation it's next to impossible to prevent any and all instability (glitches), there are a few things you can do to avoid or minimize these issues.

- If possible, do not allow jointed bodies to collide with one another. This is the default behavior for joints.
- Use the *Max Force* setting to limit the amount of force a joint can exert on its bodies. This is very effective to prevent joints from "exploding".
- The *Stiffness* of Spring Joints should be reasonably low, or combined with a reaonable *Max Force* setting.
- The *Maximum Distance* of Distance Joints, if enabled and *Collide Bodies* is enabled as well, must be far enough away from both bodies so that they can freely pass by each other.
- Write code that detects a problematic situation and gracefully resolves it. This is a last resort measure, but not uncommon.
