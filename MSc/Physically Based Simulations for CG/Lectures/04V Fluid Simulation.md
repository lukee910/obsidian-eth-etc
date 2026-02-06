#TODO: Fill in the blanks overall

#TODO: Recap vector fields

Fluids, smokes, emulsions, ...

Commonality: Zero shear modulus (cannot resist any shear force applied to them, flow instead)

Note: We'll not look at liquids, mostly gasses (liquids have some tricky edge conditions)
## Calculus Review
### Functions & Gradients
#TODO: Slide 6
Note: $\nabla f^{T} \Delta x$ change can be written as a dot product!
### Vector Fields
Vector field assigns a vector to every point in space
$$
\mathbf{u}(x,y,z) = \left( u(x,y,z), v(x,y,z), w(x,y,z) \right)^{T}
$$
### Divergence
How much vectors diverge at a certain point. Can tell us if it's a source or a sink.

[[Divergence (Nabla *)|Divergence]]
### Curl
How fast vector field is rotating around a given point.
$$
\nabla \times \mathbf{u} = \nabla \times (u,v,w) = \left( \frac{\partial w}{\partial y} - \frac{\partial v}{\partial z}, \frac{\partial u}{\partial z} - \frac{\partial w}{\partial x}, \frac{\partial v}{\partial x} - \frac{\partial u}{\partial y} \right)^T
$$
This can tell us if the field is incompressible (which we want for fluids). Notably, check $\nabla \varphi$ for compressibility: 
![[Curl Helmholtz decomp..png]]
### Laplacian
Laplacian is the composition of gradient and divergence operators.
$$
\nabla^{2} f = \nabla \cdot \nabla f = \frac{\partial^{2} f}{\partial x^{2}} + \frac{\partial^{2} f}{\partial y^{2}}+ \frac{\partial^{2} f}{\partial z^2}
$$
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
#TODO: Cauchy Momentum Equation
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
### Interpreting Pressure and Viscosity Terms
#TODO: This.
### Plugging In
#TODO: This.
(On slide: Outlined term is what doesn't line up yet)
### Eulerian vs Lagrangian
#### Eulerian
Compute how quantity $q$ changes locally in time and space.
Look at: Partial derivatives $\frac{\partial q}{\partial t}$ and $\frac{\partial q}{\partial x}$.
#### Lagrangian
Compute how $q$ changes when following given particle / material point.
Look at: Total derivatives $\frac{dq}{dt}$.

Function only depends on time, since $q$ depends on $x,t$, but $x$ is a function of $t$.

#TODO: Material Derivative $Dq/Dt$

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