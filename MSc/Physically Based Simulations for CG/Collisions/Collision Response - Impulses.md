Idea: Correct the velocity applied to never intersect.

Reference: Robust Treatment of Collisions, Contact and Friction for Cloth Animation, Bridson et. al., 2002.
## Basic Algorithm
#TODO: Algorithm slides 11 slide 27
## Invariant
Must never have intersections.
## Proximity
#TODO: Slides 11 Slide 30

Idea: Always maintain a distance $>\varepsilon_{close}$ between any triangles.

Note: Velocity change on $x_{b}$ cannot be applied directly, have to distribute this over the vertices.
### Problem - Convergence
Proximity-based impulses alone cannot prevent all collisions. Moving stuff can cause other intersections, have to loop and hope it converges decently. We usually just do a few iterations and hope.
## Continuous Collision Detection
Problems can happen when an object completely moves through another one during a step. [[Collision Response - Impulses#Proximity]] cannot detect that.

Solution: [[Continuous Collision Detection]]
## Fail-Safe
If intersections are left: [[Rigid Impact Zones]]

Improvement: [[Inelastic Projections]]
## Limitations
- Intersection recovery [[#Recovering from Intersections]]
- Decoupling between physics and collision handling
	- Impulses introduce large deformations, which stabilize
	- Limits step size
### Recovering from Intersections
Because of the invariant, impulse based collision responses CANNOT recover from intersections as-is.

Some approaches:
- Find intersecting regions in global analysis
	- Either don't do impulses or use attractions for those regions
- Contour minimization
