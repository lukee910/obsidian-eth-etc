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
* 
Where:
$$
\sigma(x) \cdot n = \begin{pmatrix}
\sigma_{x} & \tau_{xy} & \tau_{xz} \\ \tau_{xy} & \sigma_{y} & \tau_{yz} \\ \tau_{xz} & \tau_{yz} & \sigma_{z}
\end{pmatrix}
$$
...we get the strong form governing PDE for stress:
$$
\nabla \cdot \sigma + f^{b} = 0
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


