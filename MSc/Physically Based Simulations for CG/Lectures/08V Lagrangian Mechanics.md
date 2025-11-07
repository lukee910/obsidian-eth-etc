Alternative to [[08V Articulated Rigid Bodies, Multi-Body Systems]]

## General Recipe
- Choose a set of generalized coordinates $q$ that describe the system
	- Independent and completely determine the configuration of the system
	- Use the generalized coordinates to define the cartesian coordinates of any point in the system we are modeling. $x(q)$ must be explicitly specified. The derivatives of that map gives the velocities.
- Write down kinetic and potential energies $K,\ U$.
- Write down Lagrangian $L:= K - U$
- Dynamics are then given by Euler-Lagrange equation: $\frac{d}{dt}\frac{\partial L}{\partial \dot{q}} = \frac{\partial L}{\partial q}$
### Example: Arm $q$
All we care about is the angle of the elbow joint. This angle alone already fully determines the system.
### Example: Particle moving under Gravity
![[Lagrangian Particle under Gravity.png|250]]
- Generalized coordinates: $q := x$ (identity map)
- Kinetic energy: $K = \frac{1}{2}\dot{x}^{T}m\dot{x}$
- Potential energy: #TODO 
- Lagrangian: $L := K - U$
- Equations of motion: #TODO: This
	- We get $F = m\ddot{x}$ ($\sim F=ma$, the usual)
### Example: Pendulum
![[Lagrangian Mechanics Pendulum.png|200]]
- Generalized coordinates: $q := \theta$
	- $L$ is fixed, positions are derived from that angle.
	- $x(q) = \begin{bmatrix} L \sin q \\ -L \cos q \end{bmatrix}$; $\dot{x}(q) = \begin{bmatrix}L \cos q \\ L \sin q\end{bmatrix} \dot{q}$.
- Kinetic energy: $K = \frac{1}{2}\dot{x}^{T} m \dot{x} = \frac{mL^{2}}{2} \dot{q}^{2}$ (via $x(q)$)
- Potential energy: #TODO: This
- Lagrangian: $L := K - U$
- Equations of motion: $\frac{d}{dt}\frac{\partial L}{\partial \dot{q}} = \frac{\partial L}{\partial q} \Rightarrow \ddot{q} = -\frac{g}{L} \sin q$.
	- Still $F=ma$ style, but express not in cartesian coordinates, but some other space.
	- Constraints are *directly* in the equations of motion!
	- Derivation is left as an exercise
### Example: Many connected particles
![[Lagrangian Mechanics Human.png|200]]
- Generalized coordinates: $q := [x_{root}\ \theta_{1}\ \theta_{2}\ \ldots]$
	- Lengths $L_{i}$ are fixed
	- $x(q) = [x_{root}\ x_{1}\ x_{2}\ \ldots]$ and $\dot{x} = \frac{\partial x}{\partial q} \dot{q} = J\dot{q}$ are computable via forward kinematics
- Kinetic energy: #TODO: This
- Potential energy: $U = -F^{T}x$
- Lagrangian: $L := K - U$
- Equations of motion: $\frac{d}{dt}\frac{\partial L}{\partial \dot{q}} = \frac{\partial L}{\partial q}$
	- #TODO: Derivations?
	- We get: $J^{T}MJ \ddot{q} + J^{T}M\dot{J}\dot{q} = J^{T}F$
		- $J^{T} M J$ is the generalized mass matrix $M(q)$
		- $J^{T}M\dot{J}\dot{q}$ are inertial effects (e.g. Coriolis and centrifugal forces, based on reference system)
		- $J^{T}F$ are generalized forces (cartesian-space forces projected into generalized coordinates) #TODO: Put this formulation up top in the theory

Same approach can be used to derive the well-known equations of motion for articulated rigid body systems:
$$
M(q) \ddot{q} + C(q, \dot{q}) = Q
$$
See: "A Quick Tutorial on Multibody Dynamics" by C. Karen Liu and Sumit Jain for a full derivation.
## Conclusion
- Elegant formulation based on generalized, or reduced coordinates
	- Allows us to completely eliminate certain types of constraints, e.g. hard constraints of joints being joined are encoded into the equations of motion, we cannot even express how to break them
- You can work out the dynamics of a rigid body using Lagrangian mechanics
	- Derive what we did last week in [[07V Rigid Body Dynamics]]
	- etc.

