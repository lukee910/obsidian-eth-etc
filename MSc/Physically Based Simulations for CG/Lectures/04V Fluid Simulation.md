#TODO: Fill in the blanks overall

#TODO: Recap vector fields

Fluids, smokes, emulsions, ...

Commonality: Zero shear modulus (cannot resist any shear force applied to them, flow instead)

Note: We'll not look at liquids, mostly gasses (liquids have some tricky edge conditions)
## Calculus Review
### Functions & Gradients
Note: $\nabla f^{T} \Delta x$ change can be written as a dot product!
[[Gradient (Nabla)|$\nabla$]]
### Vector Fields
[[Vector Field]]
### Divergence
How much vectors diverge at a certain point. Can tell us if it's a source or a sink.

[[Divergence|Divergence ($\nabla \cdot$)]]
### Curl
How fast vector field is rotating around a given point.
[[Curl]]
### Laplacian
[[Laplacian]]
## Modeling Fluid Dynamics
[[Navier Stokes Equation#Incompressible]]

This chapter basically derives the [[Navier Stokes Equation]].
### Incompressibility
[[Navier Stokes Equation#Incompressibility Condition]]
Incompressibility means, that any region $\Omega$ must preserve its volume. Equivalently, net flux through boundary $\partial \Omega$ with normal $\mathbf{n}$ must be $0$.

Note: Gasses are compressible, but at CG speeds, we can pretend they're not. Makes our lives easier.
### Momentum Equation
[[Navier Stokes Equation#Momentum Equation]]
Recall: Momentum = mass times velocity

#### Cauchy Momentum Equation
[[3D Stress#Governing PDE for Stress]]:
$$
\nabla \cdot \sigma + f^{ext} = 0
$$

There we get the Cauchy Moment Equation:
$$
\rho \frac{du}{dt} = \nabla \cdot \sigma + f^{ext}
$$
Note:
- This generalizes the governing PDE to a dynamic equilibrium, i.e. particles are allowed to move.
#### Stress
Question: What form does $\sigma$ take for fluids?
$$
\sigma = \tau - pI
$$
Where:
- See [[3D Stress#Cauchy's Stress Theorem]] for $\tau, \sigma$
- $p = \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz})$ pressure is the negative mean **normal stress**.
	- Pressure: Whatever it takes to make the velocity field divergence-free
- $\tau = \sigma + p I$ deviatoric part, traceless, describes **visocous stress**.
	- Viscosity:
		- Resists relative motion in fluid proportional to [[Laplacian|Laplacian ($\nabla^2$)]]
		- Visually, how far from average is the velocity at a given location?
#### Stokes' Assumption
* Stress depends linearly on velocity gradient $\mathbf{u}$.
* Fluid is isotropic (same in all direction)
#### Form of Stress
Viscous stress takes a form analogous to linear-elastic isotropic solids:
$$
\mathbf{\tau} = \mu(\nabla \mathbf{u} + (\nabla \mathbf{u})^{T)}+ \lambda(\nabla \cdot \mathbf{u}) \mathbf{I}
$$
For incompressible fluids, this leads to:
$$
\tau = \mu(\nabla \mathbf{u} + (\nabla \mathbf{u})^T)
$$
Divergence of $\tau$ follows as Laplacian of $\mathbf{u}$:
$$
\nabla \cdot \tau = \mu \nabla \cdot \nabla \mathbf{u}
$$
### Checkpoint: Viscous Stress and Cauchy Momentum
By combining $\sigma = \tau - pI$, $\tau = \mu(\nabla \mathbf{u} + (\nabla \mathbf{u})^T)$ and the [[#Cauchy Momentum Equation]], we get:
$$
\rho \frac{du}{dt} = \nabla \cdot \sigma + f^{ext} = -\nabla p + \mu \nabla^{2}u + f^{ext}
$$
Not quite at the [[Navier Stokes Equation]] yet: Should be $\frac{\partial u}{\partial t} + u \cdot \nabla u$ on the left hand side.
### Eulerian vs Lagrangian
#### Eulerian
Compute how quantity $q$ changes locally in time and space.
Look at: Partial derivatives $\frac{\partial q}{\partial t}$ and $\frac{\partial q}{\partial x}$.
#### Lagrangian
Compute how $q$ changes when following given particle / material point.
Look at: Total derivatives $\frac{dq}{dt}$.

Function only depends on time, since $q$ depends on $x,t$, but $x$ is a function of $t$.

$$
\frac{dq_{i}}{dt} = \frac{\partial q}{\partial t} + \frac{\partial q}{\partial x_{i}}\frac{\partial x_{i}}{\partial t} = \frac{\partial q}{\partial t} + u_{i}\cdot \frac{\partial q}{\partial x} = \frac{Dq}{Dt}
$$
$\frac{Dq}{Dt}$ is the material derivative, the rate of change of $q$ belonging to a given material/fluid element (particle) moving within a material/fluid.
### Vector Quantities
* Same equation applies to vector quantities (e.g. colour, velocity, density, ...)
* For Navier Stokes: Advect velocity ($\mathbf{u} \cdot \nabla \mathbf{u}$).
### Plugging in, again
#TODO: Plug into Cauchy Momentum Equation. Then we get the Navier Stokes Equation.
## Boundary Conditions
[[Navier Stokes Equation]] describes equilibrium conditions inside the medium.

Three types of boundary conditions for solid objects:
* For non-moving boundaries, we have: $\mathbf{u} \cdot \mathbf{n} = 0$
* Moving boundaries: $\mathbf{u} \cdot \mathbf{n} = \mathbf{u}_{\text{solid}} \cdot \mathbf{n}$
* For viscous fluids, impose no-slip condition: $\mathbf{u} = \mathbf{u}_{\text{solid}}$
	* Fluid gets "dragged" along the side of the moving object, sticks to it
## Solving the Navier Stokes Equations
Some issues, we have constraints, not just PDEs!

Approximations $\to$ Stable Fluids.

Approach: Split into steps:
* Advection
* Viscosity
* External Forces
* Pressure

Note: Order of steps matter
* Want: Divergence-free flow
* Advecting compressible fields causes material loss/gain.
### Spatial Discretization
* Regular grid with size $\Delta x$.
* Pressure $p_{i,j}$ and velocities $\mathbf{u}_{i,j} = (u_{i,j}, v_{i,j})$ are stored at grid nodes $\mathbf{x}_{i,j}$ (collocation).
* Spatial derivatives at nodes with finite differences
Three approaches: #TODO: Formulas on slide 33
* Forward Difference
* Backward Difference
* Central Difference
#### Collocation Problems
Grids with collocation and central differences have other solutions to the real ones.

Solution: Staggered Grids
#### Staggered Grids
MAC (Marker and Cell) Grid.

* Pressure $p_{i,j}$ is at the center of the grid.
* $x$-part of velocity $u_{\frac{i+1}{2}, j}$ in middle of $x=const$ face.
* $y$-part of velocity $v_{i, \frac{j+1}{2}}$ in middle of $y=const$ face.
* Velocity derivatives at cell centers are computed using centered differences.
### Advection
#TODO: This

Central idea of stable fluids paper: Solve lagrangian equation $\frac{Du}{Dt} = 0$ with particles $\Rightarrow$ Lagrangian advection.

#TODO: Forward vs backward ideas. Note: Look from grid point to find $x_{source}$.

#### Integrating Body Forces

#### Integrating Pressure Forces
Note: Why we are taking the gradient is, because we don't yet have the pressure for the new position (which would be needed to directly do Explicit Euler).

#TODO: What is in which step of stable fluids?

#TODO: Book referenced