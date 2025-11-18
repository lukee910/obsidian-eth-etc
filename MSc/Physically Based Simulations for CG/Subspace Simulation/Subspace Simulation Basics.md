## Setup
Full-space equations of motion:
$$
M\ddot{u} + D\dot{u} + Ku = f(t)
$$
- $M$: Mass matrix
- $D$: Damping (?)
- $K$: Stiffness Hessian

Reduced coordinates:
$$
u = Uq
$$
For $U \in \mathbb{R}^{3n \times r}$ linear basis

Insert both:
$$
MU\ddot{q} + DU\dot{q} + KUq = f(t)
$$

Project onto the subspace:
$$
U^{T}MU\ddot{q} + U^{T}DU\dot{q} + U^{T}KUq = U^{T}f(t)
$$

Note: $U^{T}MU \in \mathbb{R}^{r \times r}$, i.e. the system of ODEs, is much smaller than full-space system.

Use [[Generalized Eigenvector (Subspace Simulation)]].

Use Rayleigh damping: $D = \alpha M + \beta K$

We get:
$$
U^{T}MU = I,
$$
#TODO: Slide 9 formula

## Resulting ODEs
$$
\ddot{q_{i}} + (\alpha + \beta \lambda_{i}) \dot{q_{i}} + \lambda_{i} q_{i} = v_{i}^{t} f
$$
## Pros and Cons
Pros:
- Equations decouple, can be run in parallel efficiently
- Accurate for low-frequency dynamics for small deformations
Cons:
- Basis cannot express large low-frequency deformations geometrically
	- Solutions:
		- Larger basis
		- Better basis vectors
		- Nonlinear basis
- Forces are not evaluated on the real geometry
	- Solution: Evaluate non-linear forces on full-space geometry [[Subspace Simulation with Nonlinear Forces]]
