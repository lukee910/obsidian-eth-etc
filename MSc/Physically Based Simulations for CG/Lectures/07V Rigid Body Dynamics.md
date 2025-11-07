## Rigid Body Idea
So far:
Keep track of $x$ and $v$, solve ODE $f=ma$.

Consider the spring setup. What happens as forces get stronger and stronger:
- Numerical stability?
- What happens at the limit?
Idea: Rather than trying to simulate that stiff mess, model everything as a single rigid body. Can translate and rotate, nothing else.

Problem: Nothing in the wild is really rigid!
## Representation
We only need to keep track of translation and rotation.

Choose one *reference point* and store its position explicitly (often center of mass).
### Center of Mass (COM)
$p$ (represented by black/white circle)
$$
\sum\limits_{i} m_{i} r_{i} = 0 \Rightarrow \ldots \text{TODO} = \frac{\sum\limits_{i}m_{i}x_{i}}{M}
$$
#TODO: Terms in between here
### Local coordinate frame
- Reference point at local coordinates $(0,0,0)$
- Orientation $R(t)$ (rotation)
Points in the local frame are denoted with a bar, $\bar{x}$.

// Rotations are orthonormal, columns are orthonormal basis.
### Local - Global coordinates conversion
$x$ global, $\bar{x}$ local
$x = p + R\bar{x}$

// Rotations transform vectors, so $\bar{x}$ is supposed to be the vector from the reference point to $\bar{x}$, but since reference is at $0$, it's fine.
### Intuition
- $p(t)$: Position of the center of mass at time $t$
- $R(t)$: Rotation over time
	- Consider the x-axis in body space, $(1,0,0)$, what is the direction of this vector in world space at time $t$? Answer: First column of $R(t)$.
## Velocity
// Speed vs velocity: Speed is just magnitude, a scalar
### Linear Velocity
$\frac{dx}{dt} = \dot{x}(t)$?
Because $\bar{x}$ is constant in local coordinate frame:
$$
\dot{x}(t) = \dot{p}(t) + \dot{R}(t)\bar{x}
$$
$\dot{p} \equiv v$ is the velocity of the COM (linear velocity of rigid body)
### Angular Velocity
Assume the linear velocity is $0$, but it's spinning.
- Rotation is about the COM
- Which points on the RB have 0 velocity? Answer: Points on axis of rotation.

$\omega(t)$ angular velocity
- Direction gives axis
- Magnitude gives speed of spin
### Quiz
#### 2D
#TODO: Quiz diagram
- Speed of the rigid body?
	- $|v|=|r||\dot{\theta}|$
	- Idea: #TODO
- Velocity of the rigid body?
	- Direction is an in-plane vector orthogonal to $r$
- Angular velocity?
	- $\dot{\theta}$
#### 3D
#TODO: Quiz sketch
- How fast is the corner moving?
	- Decompose $c$ into $a$ (aligned with $\omega$) and $b$ (perpendicular to $\omega$)
	- So we get $|\dot{b}|=|b||\omega|$
	- Since $\dot{b}$ is perpendicular to $\omega$, so $\dot{b} = \omega \times b$
	- Therefore: #TODO
// Using: Cross product of parallel vectors is $0$
## Back to unit meanings
### Cross product as matrix-vector product
#TODO: Matrix-vector representation of the dot product
Skew-symmetric matrix $[a]$ (skew-symmetric: Transpose is its negative)

Notated as: $a \times b = [a]b$.
### $\dot{R}$ meaning
What do columns represent?
#TODO: R dot formula
$$
\dot{R}(t) = ...
$$
Using the [[#Cross product as matrix-vector product]]:
$\dot{R}(t) = [\omega(t)]R(t)$
#TODO: Get intuition of what $\omega \times ...$ means geometrically.
### Applying $\dot{R}$ to velocity
#TODO: Slide that inserts $\dot{R}(t)$ into $\dot{x}$ formula.

Note: We have a linear component and an angular component. This decoupling will continue.

Homework: Derive $\ddot{x}(t)$ acceleration (derive $\dot{x}$).
## Rigid Body Dynamics
### Kinetic Energy of a Rigid Body
Recall kinetic energy of mass point:
$$
K = \frac{1}{2} \bar{x}^{T} m \dot{x}
$$
For a rigid body:
$$
K = \frac{1}{2} \sum\limits_{i} \bar{x}_{i}^{T} m \dot{x}_{i}
$$
But recall $\dot{x}$... #TODO: Slide of derivations
The different terms:
- 1st term: Kinetic energy due to linear motion
- 2nd term: By definition of COM, $\sum\limits_{i} m_{i} r_{i} = 0$, so this cancels.
- 3rd term: Moment of inertia tensor $I$
	- Can be described purely via local coordinates $\bar{x}$
	- $I_{b}$ moment of inertia in local coordinates
	- $I = R I_{b} R^{T}$
	- Constant in body coords, can be precomputed!

$[r_{i}]^{T} [r_{i}]$: Ends up as $r_{i}^{T}r_{i} \mathbb{I}_{3x3} - r_{i} r_{i}^{T}$.

Note that $r_{i} = x_{i} - p = p+R\bar{x}_{i} - p = R\bar{x}_{i}$.
#TODO: Idk a bunch of derivations

### Moment of Inertia in Practice
Often approximate. Approximation can be good, since it's locally constant. Approaches:
- Bounding box
- Point sampling
### Forces and Torques
$f_{i}(t)$ denotes the total force acting on the $i$th particle at time $t$. 
- Total/net force: $F(t) = \sum\limits_{i} f_{i}(t)$.
- Total/net torque ("angular force"): $\tau(t) = \sum\limits_{i} r_{i} \times f_{i}(t)$
Net *torque* depends on point of application, net *force* does not.

Force types:
- Gravity
- Springs (attached outside)
- Collisions
- Frictional contact
- Joint constraints
- Motors or muscles
- ...
#### Example: Gravity
$f_{i} = m_{i}g$
Net force and torque:
- $F = \sum\limits_{i}m_{i}g = g\sum\limits_{i}m_{i} = Mg$
- $\tau = \sum\limits_{i}r_{i}\times m_{i}g = -\sum\limits_{i}m_{i}[g]r_{i} = -[g]\sum\limits_{i} m_{i}r_{i} = 0$ (by COM definition).
### Linear and angular momenta
Note: Momenta are conserved quantities (unless acted upon)
#### Linear Momentum
$p$: Total *linear* momentum of the RB: #TODO: Derivation below
$$
p = \sum\limits_{i}m_{i}\dot{x}_{i} = \ldots = Mv
$$
#### Angular Momentum
$L$: Total *angular* momentum of the RB:
$$
L = \sum\limits_{i} r_{i} \times m_{i} \dot{x}_{i} = \ldots = I\omega
$$
#### Conversation of linear momentum
#TODO: Slide with newton's second law
#### Conversation of angular momentum
#TODO: Derivations there

Does the MoI change? Yes, in global coords, related to $R$:
$I = R I_{b} R^{T} \Rightarrow \dot{I} = \dot{R} I_{b} R^{T} + R \dot{I}_{b}R^{T} + R I_{b} + \dot{R}^{T}$

Recall $\dot{R} = [\omega]R$, so:
$$
\dot{I} = \ldots = \ldots \Rightarrow \dot{I}\omega = \omega \times I \omega
$$ #TODO: $\dot{I}$ formula derivations
$$
\Rightarrow I \dot{\omega} = \tau - \omega \times I \omega
$$
Note: Angular *acceleration* changes over time, even if the angular momentum does not.

### Equations of Motion for Rigid Bodies
$$
\begin{bmatrix}
F \\ \tau - \omega \times I \omega
\end{bmatrix} = \begin{bmatrix}
M \mathbb{I} & 0 \\ 0 & I
\end{bmatrix}
\begin{bmatrix}
\dot{v} \\ \dot{\omega}
\end{bmatrix}
$$
Roughly corresponding to $F = ma$.

Note: Linear and angular components of motion are decoupled!
## Time Stepping Scheme (Symplectic Euler)
// Symplectic: Use new velocity to update position, #TODO: Symplectic Euler in [[_T ODEs]]

At each time step:
- Compute net force $F$ and net torque $\tau$
- Update linear and angular velocities: $v_{i+1} = v_{i} + h \frac{F}{M},\ \omega_{i+1} = \omega_{i} + h I^{-1}(\tau - \omega_{i} \times I \omega_{i})$
	- #TODO: Note the inversion thing on the slide
- Update COM position: $p_{i+1} = p_{i} + hv_{i+1}$
- Update orientation:
	- Option 1: $R_{i+1} = R_{i} + h\dot{R}_{i+1} = R_{i} + h[\omega_{i+1}] R_{i} = (\mathbb{I} + h[\omega_{i+1}])R_{i}$
		- Issue: $\mathbb{I} + h [\omega_{i+1}]$ creates a non-orthonormal matrix, it's not a rotation matrix anymore!
		- Fix through Gram-Schmidt orthonormalization
			- Not unique solution, introduces errors
		- Fast, easy to parallelize, but error prone
	- Option 2:
		- Compose rotations via multiplication.
		- #TODO: Explanation
		- $R_{i+1} = Rot\left(h|\omega_{i+1}|, \frac{\omega_{i+1}}{|\omega_{i+1}|}\right)R_{i}$.
		- More precise, but slower

From here on: Last part of 08V
## Quaternions
[[Quaternions]]
## Time Stepping using Quaternions
Continues from [[#Time Stepping Scheme (Symplectic Euler)]].
### Update Orientation Step
Option 1:
$$
q_{i+1} = q(h|\omega_{i+1}|, \frac{\omega_{i+1}}{|\omega_{i+1}|})q_{i}
$$
Option 2:
#TODO:

In the limit, these two options are equivalent.

Note: For option 2, we still need to do the normalization, but it's much easier than Gram-Schmidt orthonormalization. #TODO: How.

