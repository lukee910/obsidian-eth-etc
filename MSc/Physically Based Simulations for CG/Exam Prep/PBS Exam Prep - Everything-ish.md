Lecture Topics:
1. [[_T Mass-Spring Systems]]
2. [[_T ODEs]]
3. [[_T Continuum Mechanics]]
4. [[04V Fluid Simulation]]
5. [[Constraint]]
6. [[_T Shells and Rods]]
7. [[_T Rigid Body Dynamics]]
8. [[08V Articulated Rigid Bodies, Multi-Body Systems]]
9. [[_T Subspace Simulation]]
10. [[_T Collisions]]
11. #TODO: Differentiable Simulation
## Basics
### Taylor
$y(t+h) = y(t) + hy'(t) + \frac{h^{2}}{2!}y''(t) + \ldots$
### Vector Calculus
- [[Gradient (Nabla)|$\nabla$]]
- [[Vector Field]]
- [[Divergence|Divergence ($\nabla \cdot$)]]
- [[Curl|Curl ($\nabla \times u$)]]
- [[Cross Product|Cross Product ($v \times w$)]]
- [[Laplacian|Laplacian ($\nabla^2$)]]
### Skew-Symmetric
$A$ is a skew-symmetric matrix iff $A = -A^{T}$. The skew-symmetric matrix for a vector $a$ is unique, noted $[a]$.

Relation to cross product:
$a \times b = [a]b$
### Quaternions
$q = w + xi + yj + zk$, where $i^{2} = j^{2} = k^{2} = ijk = -1$.
Often noted as $q = [w, v]$, where $v = \begin{pmatrix}x \\ y \\ z\end{pmatrix}$.
#### Rotation Quaternions
$q(\theta_{a}, v_{a})$ (rotate around $v_{a}$ by $\theta_{a}$): $q = \begin{bmatrix}w \\ v\end{bmatrix} = \begin{bmatrix}\cos \frac{\theta_{a}}{2} \\ \sin \frac{\theta_{a}}{2} v_{a} \end{bmatrix}$
Rotate vector $v$ around $q=q(\theta_{a}, v_{a})$: $Rot(v, q) = qv = q \cdot (0, v) \cdot q^{-1}$.
## Mass Spring Systems
[[_T Mass-Spring Systems]]
[[Mass-Spring Systems - Overview]]
### Takeaways
- Deformable bodies
- Deformation force is linear
- Have to apply damping
	- [[Mass-Spring Systems - Overview#Linear Damping Force|Linear]]:
	  $f^{visc} = -\gamma v$
		- Simple, but also dampens rotation etc.
## Solving ODEs, Integration Schemes
- Notation
	- $y(t)$: True solution
	- $y_{i}$: Approximate solution at $t = t_{0} + i \cdot h$
	- $h$: Time step size
	- $f(t_{n}, y_{n}) = y'(t_{n})$
		- Alternative notation online: $f(t_{n}, y(t)) = y'(t_{n})$
- Error
	- Global Error: $|y_{i} - y(t_{i})|$
		- True error at any given timestep
	- Local Error: $\left| \left( y_{n} + \int^{t_{n+1}}_{t_{n}} f(t, y(t)) dt \right) - y_{n+1} \right|$
		- $\int^{t_{n}}_{t_{n+1}} f(t, y(t)) dt$: Real step size
		- Error of step $t_{n} \to t_{n+1}$
	- [[Evaluating and Comparing Integration Schemes#$p$-Accuracy]]: Local Error $\mathcal{O}(h^{p+1})$ is $p$ accurate
- Integration Schemes
	- Explicit Euler
		- "Assume no change in $y'$"
		- $y_{n+1} = y_{n} + hf(t_{n}, y_{n})$
		- First-order accurate ($\mathcal{O}(h^{2})$ error)
	- Explicit Midpoint
		- "Maybe $y'$ at the midpoint is better?"
		- $y_{n+ \frac{1}{2}} = y_{n} + \frac{h}{2} f(t_{n}, y_{n})$
		- $y_{n+1} = y_{n} + h f(t_{n+ \frac{1}{2}}, y_{n+ \frac{1}{2}})$
		- Second-order accurate
	- Implicit Euler
		- "Maybe $y'$ at the next step is better?"
		- $y_{n+1} = y_{n} + f(t_{n+1}, y_{n+1})$
		- First-order accurate
	- Symplectic Euler
		- Applied to pair of ODEs:
			- $\frac{dx}{dt} = f(t, v)$
			- $\frac{dv}{dt} = g(t, x)$
		- $v_{n+1} = v_{n} + g(t_{n}, x_{n}) h$
		- $x_{n+1} = x_{n} + f(t_{n}, v_{n+1}) h$
		- First-order accurate
	- Comparison
		- Explicit Euler: Tends to explode.
		- Explicit Midpoint: Slower (more evaluations).
		- Implicit Euler: Tends to lose energy.
		- Symplectic Euler: Conserves momentum, almost conserves energy.
- Equation Solving: Newton's Method
	- $g(x_{n})$: Energy (or anything else to optimise)
	- Goal: Solve $g(x_{n+1}) = 0$
		- Example: [[_T Mass-Spring Systems]]
		- Via correction: $g(x_{n+1} + \Delta x) = 0$
	- Procedure at step $x_{n+1}$:
		- Initial:
			- Make a guess, $x_{n+1} = x_{n} + hv_{n}$
		- Each loop:
			- Solve $\frac{\partial g}{\partial x} \Delta x = -g(x_{n+1})$ 
				- Linear equation, $\frac{\partial g}{\partial x}$ Jacobian matrix
			- Update $x_{n+1} \mathrel{+}= \Delta x$
			- Compute error $|g(x_{n+1})|$
				- Exit if small enough
## Continuum Mechanics
[[_T Continuum Mechanics]]
[[Continuum Mechanics Overview]]
![[CM FEM approaches.png|300]]
$\Rightarrow$ [[Discrete Energy Approach]]
### 1D
[[1D Case for Continuum Mechanics]]
* $f^{ext}$: External force applied
* $\varepsilon = \Delta l / L$: *Strain* (relative stretch)
* $\sigma = f^{int} / A$: *Stress* (internal force per area)
* Via Hooke's Law:
	* $\sigma = E \varepsilon$ ($E$ Young's Elasticity Modulus, defined via this)
	* $f = k \Delta l$
* Governing PDE:
$$
\begin{align}
E \partial_{xx} u(x) &= -f^{b}(x) \quad \forall x \in ]0,1[ \quad \text{Internal Forces} \\
E \partial_{x} u(1) &= -f^{s} \quad \text{Apply force at right boundary} \\
u(0) &= 0 \quad \text{Left boundary static}
\end{align}
$$
### 3D
[[3D Case for Continuum Mechanics]]
![[3D CM FEM setup.png]]
Note: $\bar{x}$ undisplaced, $x$ displaced. 
![[Displacement Vector Deformed.png|300]]
Displaced deformation vector $d$ in terms of original displacement $\bar{d}$: <sub>(via Taylor approximation)</sub>
$$
d = x_{2} - x_{1} = \ldots = (I_{n} + \nabla u) \bar{d}
$$

![[3D Case for Continuum Mechanics#Deformation Gradient]]
### Strain
[[3D Nonlinear Strain]]
Measure the change in length square by deformation in any given direction.
- Green Strain: $E = \frac{1}{2}(F^{T}F - I)$
	- Quadratic in $\nabla u$
		- $E = \frac{1}{2}(\nabla u + \nabla u^{T} + \nabla u^{T} \nabla u)$
	- Pros: Invariant under rotations, more accurate
	- Cons: Expensive
- Cauchy Strain: $\varepsilon = \frac{1}{2} (F + F^{T}) - I$
	- Linear in $\nabla u$
		- $\varepsilon = \frac{1}{2} (\nabla u + \nabla u^{T}) - I$
	- Pros: Simpler, Cheaper
	- Cons: Rotation artifacts, less accurate
- Use Green if you want precision, Cauchy only if you must
### Stress
[[3D Stress]]
Measure the force per area caused by the deformation. $t(x, n) = \frac{df}{dA}$ as $A \to 0$.
![[3D CM FEM Stress Setup.png|150]]
Cauchy's Stress Theorem: $t(x, n) = \sigma(x) \cdot n$
- $\sigma_{i}$: Normal stress
	- Elastic stretching force per area
* $\tau_{ij}$: Shear stress
	* Force in direction $i$ induced by stretching in direction $j$
Where:
$$
\sigma(x) \cdot n = \begin{pmatrix}
\sigma_{x} & \tau_{xy} & \tau_{xz} \\ \tau_{xy} & \sigma_{y} & \tau_{yz} \\ \tau_{xz} & \tau_{yz} & \sigma_{z}
\end{pmatrix}
$$
...we get the strong form governing PDE for stress:
$$
\nabla \cdot \sigma + f^{ext} = 0
$$
(But instead [[Discrete Energy Approach]]. See [[Linear Elasticity Model]])
### Elasticity Models
#### Linear Elasticity
[[Linear Elasticity Model]]
Idea: Energy density $\Psi = \frac{1}{2} \lambda\ tr(\varepsilon)^{2} + \mu\ tr(\varepsilon^{2})$ defines material properties. Stress derives directly from this.
Cauchy stress: $\sigma = \frac{\partial\Psi}{\partial\varepsilon} = \lambda tr(\varepsilon)I + 2 \mu \varepsilon$.
- $tr(\varepsilon^{2}) = \|\varepsilon\|_{F}^{2}$ penalizes all stress components equally
- $\lambda\ tr(\varepsilon)^{2}$ penalizes volume changes (dilatations)
- Use material parameters $\mu,\lambda$
#### Nonlinear Elasticity
[[Nonlinear Elasticity]]
- St. Venant Kirchhoff (StVK)
	- Replace Cauchy with Green strain
	- $\Psi_{StVK} = \frac{1}{2} \lambda\ tr(E)^{2} + \mu\ tr(E^{2})$
	- Problems
		- No hard barriers, i.e. can be deformed into 0 volume / inversion with finite energy
		- Softens under compression #Unclear 
- Neo-Hookean
	- $\Psi_{NH} = \frac{\mu}{2}(tr(C) - 3) - \gamma \ln(J) + \frac{\mu}{2} \ln(J)^{2}$
	- With:
		- $C = |F|^{2}_{F}$
		* $J = \det F$
	* Solves StVK problem of inversion
	* Good for up to ~20% deformation
## Finite Elements Method
[[Finite Element Discretization]]
Instead of calculating stress, strain, deformation on continuous setting as above, approximate with some finite elements. Also, skip strong form for calculations.

A finite element consists of:
- A closed subset $\Omega_{e} \subset \mathbb{R}^d$ with $n$ vectors of nodal positions $\bar{x}_{i} \in \mathbb{R}^{d}$ describing the reference geometry.
- $n$ vectors of degrees of freedom (e.g., deformed positions $x_{i}$).
- $n$ nodal basis functions $N_{i} : \Omega_{e} \to \mathbb{R}$.
	- Note: $N_{i}(\bar{x}_{j}) = \delta_{ij}$, i.e. must be $1$ at their node and $0$ at other nodes.
	- Interpolate between that.
We get as Deformation Gradient:
$$
F = I + \frac{\partial u(\bar{x})}{\partial \bar{x}} = \frac{\partial x(\bar{x})}{\partial \bar{x}} = \sum\limits_{i} x_{i} \left( \frac{\partial N_{i}}{\partial \bar{x}} \right)^{T}
$$
Note:
- $F$ linear in $x_{i}$
- $F$ constant across an element (e.g. tetrahedron)
## Fluid Simulation
[[04V Fluid Simulation]]
![[Navier Stokes Equation]]

Note: We consider **gasses** incompressible here, treat them the same as fluids.

### Cauchy Moment Equation
$$
\rho \frac{du}{dt} = \nabla \cdot \sigma + f^{ext}
$$
### Stress
$$
\sigma = \tau - pI
$$
- $p = \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz})$ pressure is the negative mean **normal stress**.
	- Pressure: Whatever it takes to make the velocity field divergence-free
- $\tau = \sigma + p I$ deviatoric part, traceless, describes **viscous stress**.
	- Viscosity:
		- Resists relative motion in fluid proportional to [[Laplacian|Laplacian ($\nabla^2$)]]
		- Visually, how far from average is the velocity at a given location?
### Eulerian vs Lagrangian
- Eulerian
	- Compute quantity $q$ at a location in time and space
	- Partial derivatives $\frac{\partial q}{\partial t}, \frac{\partial q}{\partial x}$
- Lagrangian
	- Compute quantity $q$ for given particle
	- Total derivatives $\frac{dq}{dt}$
- Material Derivative $\frac{Dq}{Dt}$: Determines the rate of change of $q$ for a given particle as it moves through the material/fluid
### Solving Navier Stokes
- Constraints (Boundary Conditions)
	- Following conditions must hold at that boundary, with $n$ the normal of the boundary
	- Non-moving boundaries: $u \cdot n = 0$
	- Moving obstacles: $u \cdot n = u_{solid} \cdot n$
	- No-slip condition (viscous fluids): $u = u_{solid}$
		- Fluid gets "dragged" along the side of the moving object, sticks to it
- Steps: Solve advection, then viscosity, then external forces, then pressure. Then repeat.
#### Advection
- Discretisation
	- Regular grid: Store pressure $p_{i,j}$ and velocity $u_{i,j} = (u_{i,j}, v_{i,j})$ at points $x_{i,j}$
		- Problems with collocation, like [[Aliasing (Graphics)]]
	- Staggered Grid (MAC Grid; Marker and Cell)
		- Pressure $p_{i,j}$ is at the centre of the grid.
		* $x$-part of velocity $u_{\frac{i+1}{2}, j}$ in middle of $x=const$ face.
		* $y$-part of velocity $v_{i, \frac{j+1}{2}}$ in middle of $y=const$ face.
		* Velocity derivatives at cell centers are computed using centred differences:
$$\frac{\partial u}{\partial x}(x_{i,j}) = \frac{u_{i+\frac{1}{2}, j} - u_{i-\frac{1}{2}, j}}{\Delta x}$$
		* Problem: Where does the particle go? $\Rightarrow$ Lagrangian Advection
* Lagrangian Advection
	* Solve Lagrangian equation $\frac{Du}{Dt} = 0$ 
	* Look backward in time from grid point to see where data comes from, interpolate at previous time
#### Viscosity
Solve viscous ODE. Leads to sparse linear system:
$$
\left( I - \frac{\Delta t \mu}{\rho} \nabla^{2} \right) u_{new} = u_{old}
$$
#### External Forces
Usually okay to do with [[Solving ODEs#Explicit Euler]].
#### Pressure
From [[Poisson Equation]] for unknown pressure, get one equation per cell. Sparse system of linear equations, use sparse solver.
## Constraints
[[_T Constraint Materials]]
### Constraint
[[Constraint]]
A constraint $C(x_{1}, \ldots, x_{n}) : \mathbb{R}^{3n} \to \mathbb{R}$ is:
- A scalar-valued function of one or several arguments
- An implicit expression for a relation that must hold between its arguments

Note: Constraint should be convex, because otherwise we get a mess.

Convention: $C(x) = 0 \Leftrightarrow$ Constraint satisfied
### Penalty Function, Penalty Force
[[Penalty Function]]
Potential energy function that can be derived (negative gradient, $-\frac{\partial E_{C}}{\partial x_{j}}$) to get the [[Penalty Force]].
Types:
- Polynomial, especially quadratic
	- The easy choice
	- Do not prevent constraint violations
- Barrier Functions
	- $P_{lb}(x) = -k \ln C(x)$
	- Infinite energy to violate constraint
	- Highly nonlinear, must be used carefully

[[Penalty Force]]: Force applied to system to improve constraint.
### Constraint Misc
- Locking
	- Prevention of bending because edges would have to be compressed
	- Cloth only easily bends if edges are aligned to bending direction
### Constraint Methods
#### Position Based Dynamics
1. Step: Unconstrained step
2. Project: Iterate over constraints, apply local corrections, reduce constraint violation
##### Strain Limiting
- Edge-based strain limiting
	- + Good for cloth sim
	- - Mesh-dependent
	- - Limits are the same in each direction
#### Projective Dynamics
Between [[#Position Based Dynamics]] and [[#Finite Elements Method]].

Idea:
- Given current configuration $x$
- For each constraint
	- Find closest configuration $p$ on constraint manifold (i.e. $p_{i}=\arg\min_{C_{i}(p)=0} d(x, p)$)
- Find new configuration that is closest to all $p_{i}$
	- Linear solve a large system with all $p_{i}$

Note:
- $p$: Auxiliary variables, don't always have to be the same as the $x$
	- E.g. take $p$ vectors of spring rest length instead of positions $x$
- $d$: Distance function
	- Some conditions, #Unclear 

Note:
- Convergence:
	- More iterations than Newton's Method, but each iteration faster
	- Linear convergence (vs Newton's Quadratic, if close to solution)
- + Convergence much better than [[#Position Based Dynamics]] and initially better than Newton's Method
- - Not as accurate as [[#Finite Elements Method]]
- - Damping if terminated too early
- - Not meant for hard constraints
#### Fast Projection
Idea:
- Find $\delta x_{i}$ vector to nearest configuration with satisfied constraint
- Take gradient of constraints at current configuration, assume $C(x_{i} + \delta x_{i}) \approx C(x_{i}) + \nabla C(x_{i})\delta x_{i}$
- Whack those constraints together and solve
- Repeat (optional)

Note:
- + Enforces hard constraints after single linear solve
- - May not get closer after that initial step
- - Doesn't find optimal solution (i.e. closest configuration)
#### Nonlinear Programming
- Solve inequality constraints as nonlinear programming
- Solves Locking
- - Slow to converge
#### Constraint Method Overview
[[#Position Based Dynamics]]:
- Fast
- Constraints not really enforced
[[#Projective Dynamics]]:
- Faster than PBD
- No strict constraint enforcement
[[#Fast Projection]]:
- Fast initial guess, but convergence not guaranteed
- Strict enforcement (to first order)
[[#Nonlinear Programming]]
- Slow to converge
- Good for preventing locking
## Shells and Rods
[[_T Shells and Rods]]
### Shells
- Shells: Surface-like flexible objects
- Deformations:
	- Stretching (in-plane)
	- Bending (out-of-plane)
	- Resistance to bending weaker than to stretching
		- We get buckling (crumpled up things)
- Curvature #TODO #Unclear 
	- [[Curvature of Curves]]
		- $\kappa = |t'| = \gamma''^{T} n = t'^{T} n$
	- $\kappa_{n}(x)$: Normal curvature (scalar): Curvature of the normal at that point
	- $\kappa_{1} = \min_{t} \kappa_{n}(t)$
		- $t$ unit vector in tangent plane
	- $\kappa_{2} = \max_{t} \kappa_{n}(t)$
	- Mean curvature: $H = \frac{1}{2}(\kappa_{1} + \kappa_{2})$
		- Depends on bending
	- Gaussian curvature: $K = \kappa_{1} \cdot \kappa_{2}$
		- Can only be changed through stretching
### Rods
E.g. for hair simulation.

[[Discrete Rods]]

#### Kirchhoff Rods
[[Kirchhoff Rods]]:
Adapted Framed Curve:
$$
\Gamma(s) = \{ \gamma(s);\ t(s), m_{1}(s), m_{2}(s) \}
$$
With:
- $\gamma$: [[#Centerline Curve]]
- $t(s) = \gamma'(s)$: Tangent, *adapted* to material frame (hence the name)
- $t(s), m_{1}(s), m_{2}(s)$: [[#Material Frame]]
![[Kirchhoff Rod Setup.png]]
## Rigid Body Dynamics
[[_T Rigid Body Dynamics]]
vs [[#Continuum Mechanics]], [[#Finite Elements Method]]: Not deformable

- $p$: Centre of mass
- $R$: Rotation of rigid body, rotation matrix
- Storing an RB in code:
	- $p(t)$: CoM position in time
	- $R(t)$: Rotation in time
- Point on a rigid body:
	- $\bar{x}$: Local coordinates (assumed given, origin at centre of mass)
	- $x$: global coordinates, $x = p + R\bar{x}$
	- Versus: [[#Continuum Mechanics]] displacement vectors
- $r, \bar{r}$: Sometimes used instead of $x$. Same meaning.
### Spin to Win
#### Angular Velocity
Spin, $\omega(t)$
- Direction of $\omega$ gives the axis that the RB is rotating around
- Magnitude of $\omega$ gives the speed at which the RB is spinning ($\left[\frac{rad}{s}\right]$)
#### Moment of Inertia
$I$. "Angular mass" for rotational part of RB's motion. Constant in body coordinates, can be precomputed. In world coordinates: $I = RI_{b}R^{T}$.

Getting $I_{b}$: Analytical solutions exist, but often just do point sampling to get an estimate.
#### Torque
Angular force. $\tau(t) = \sum\limits_{i} r_{i} \times f_{i}(t)$ ("Lever where the force is applied times the force itself").

Net(=total) torque depends on the point where a force is applied, but net force does not.
### Articulated Rigid Bodies
Joint: Join two points on two rigid bodies, $x_{a} = p_{a} + R_{a}\bar{r}_{a}$, $x_{b} = p_{b} + R_{b}\bar{r}_{b}$. For example, $x_{a} = x_{b}$ as the goal.

Approaches:
- Springs (0 rest length)
	- High stiffness required to actually come close
		- High stiffness causes numerical issues
- Constraint (0 distance as target)
	- General formulation, works well
### Lagrangian Mechanics
vs [[#Articulated Rigid Bodies]]

Elegant formulation on reduced coordinates.

Recipe:
- Choose a set of generalized coordinates $q$ that describe the system
	- Independent and completely determine the configuration of the system
	- E.g. the angle of a pendulum (instead of the position directly)
	- Must have map to position: $x(q)$
- Write down kinetic and potential energies $K,\ U$.
- Write down Lagrangian $L:= K - U$
- Dynamics are then given by Euler-Lagrange equation: $\frac{d}{dt}\frac{\partial L}{\partial \dot{q}} = \frac{\partial L}{\partial q}$

For many particles, the generalized coordinates $q$ contain information for all particles, combined somehow. E.g. $q = [ x_{root}, \theta_{1}, \theta_{2}, \ldots]$ for a set of particles connected by unit length edges, this gives us all information for the entire system.
## Subspace Simulation
Idea: Find a low-dimensional subspace that captures likely/desired behaviour, simulate that subspace.
### Low-Frequency Deformations
Idea: These deformations that are easy to induce.

Linear Modes: Deformations corresponding to the eigenvectors of the optimization problem.

Notes:
- + Fast to solve
- + Accurate for:
	- Low frequency deformations
	- Small deformations
- - Inaccurate for:
	- Large deformations
	- Rotations
### Summary
Other methods exist to choose a better basis and non-linear spaces. Anyways.

- + Accelerate
- + Fast independent of model complexity
- - Expensive pre-computations
	- Need to be redone when geometry/material changes
- - Motion that doesn't match the chosen basis is not captured
## Collisions
[[_T Collisions]]

Collision Handling = Collision Detection + Collision Response

### Collision Detection - Broad and Narrow Phase
Idea:
1. Broad: Get potentially colliding triangle pairs (PCTP)
	1. Bounding volumes
2. Narrow: Perform distance test on PCTPs

Broad:
[[Collision Detection - Bounding Volumes]]

Narrow:
- Triangle-triangle distance
- Edge-edge distance
- Distance problem
	- Optimisation problem
	- Quadratic problem
### Continuous Collision Detection
Idea: Don't miss collisions during timesteps.
### Collision Handling
#### Impulse-Based Collision Response:
- Step ignoring collisions
- Correct positions with a force

Note:
- NEEDS that the initial configuration doesn't have collisions,!
- Cannot reliably prevent intersections
	- Collisions may be missed across a timestep
- Cannot recover from intersections
#### Inelastic Projections
Idea: Minimize the length of the intersection contour (outline) between two meshes.

Can often, but not always recover.
### Coupling Physics and Collisions
#### Incremental Potential Contact (IPC)
- Smoothly clamped, locally supported barrier function for collision penalties.
	- Continuous collision condition
- Intersection aware line search for the step newton iteration
	- Just making the energy smaller is not good enough
	- Have to do [[Continuous Collision Detection]] during each newton step.
## Differential Simulation
"How does a change in parameters affect the outcome of the simulation model?"
- Targeted animation, control
- Machine Learning

Simulation setup:
Parameters $p$ $\rightarrow$ Equilibrium state $x(p)$, where $x(p) = \arg\min_{x} W(x, p)$, $W$ potential energy. Then, derive $\frac{\partial x}{\partial p}$ somehow.

Solve with gradient descent, but slow.
- BFGS: Quasi Newton Method.
- Gauss-Newton: Second Order Newton's Method.

Quasi Newton Method: Like the Newton's Method but using an approximation for the derivative instead of the real one.

