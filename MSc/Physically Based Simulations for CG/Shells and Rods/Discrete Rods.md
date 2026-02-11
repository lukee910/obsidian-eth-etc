How to discretise rods?

Approaches:
- Centerline + Material Frame
	- $\gamma(s), m_{1}, m_{2}\ \Rightarrow$ 9 degrees of freedom
	- Adapted adds 1 constraint, orthogonal adds 2, normalized adds 3, left with 3 DoF
	- Complicated to maintain the constraints
- Curvature + Twisting
	- Minimal representation
	- Implicit centerline
		- Has to be reconstructed, non-trivial with twist in it
- Centerline + Angle
	- Implicit reference frame, reconstructed via angle
## Centerline and Angle Representation
#TODO: Quantities on slide 36
#TODO: Slide 38

## Energy
#TODO: Slide 39

Look at Bergou 2010
## Parallel Transport
Calculating the reference frame ([[Kirchhoff Rods#Bishop Natural Frame]]) 
#TODO 
### Properties and Drawbacks
- Frames depend on each other increasingly towards the end
- Forces depend on frames, which depend on geometry
	- Force Jacobian is dense
### Parallel Transport in Time
Follow-up paper. Idea: Parallel transport via forces from old edge to new frame.
#TODO: Time PT
#### Few Details for Implementing
Do update from one newton step to the next. Need to implement an implicit integration. Where?
