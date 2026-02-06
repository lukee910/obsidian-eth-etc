## Setup
![[1D continuous elasticity.png]]
* $f^{ext}$: External force applied
* $\varepsilon = \Delta l / L$: *Strain* (relative stretch)
* $\sigma = f^{int} / A$: *Stress* (internal force per area)

We have from Hooke's law: $\sigma = E \varepsilon$ ($E$: Young's elasticity modulus, scalar). Spring analogy: $f = k \Delta l$.

Note: Here we assume the other two directions are not doing anything. For real silicone, the other two dimensions would have to contract in order to preserve volume.
## Segment Deformation
![[CM 1D segment deformation with forces.png]]
Segment $[x_{i}, x_{j}]$ with $L_{ij} = x_{j} - x_{i}$ and $l_{ij} = x'_{j} - x'_{i}$.
### Displacement Field
Displacement Field: $u(x) = x' - x$ (deformed minus undeformed)
### Strain
Strain on segment: $\varepsilon_{ij} = \frac{l_{ij} - L_{ij}}{L_{ij}} = \frac{u(x_{i} + dx) - u(x_{i})}{dx}$
We have for $dx \to 0$: $\varepsilon = \frac{\partial u}{\partial x} =: \partial_{x} u$. Strain approaches the derivative of the displacement field.
### Internal Force Density
Internal force density of segment: $f_{ij}^{int} = \frac{A\sigma(x_{i} + dx) - A\sigma(x_{i})}{A \cdot dx}$, where the numerator is the total force and the denominator turns it into the density per segment.
We have for $dx \to 0$: $f^{int} = \partial_{x} \sigma = E \partial_{xx} u$ the force density at an arbitrary point.
## Equilibrium Equations
Forces:
* $f^{b}$ applied body force density
* $f^{s}$ applied surface force density
We want to have these at an equilibrium at every point.
### Equilibrium Conditions
$$
\begin{align}
E \partial_{xx} u(x) &= -f^{b}(x) \quad \forall x \in ]0,1[ \quad \text{Internal Forces} \\
E \partial_{x} u(1) &= -f^{s} \quad \text{Apply force at right boundary} \\
u(0) &= 0 \quad \text{Left boundary static}
\end{align}
$$
Governing PDE in *strong form* (strong: needs to hold in every point).

Requires second derivatives of $u$.

But: Strong form is hard/impossible to discretize.
### Equilibrium Conditions - Weak Form
$$
\begin{align}
\int^{1}_{0} E \partial_{x} u\ \partial_{x}v\ dx &= \int^{1}_{0} f^{b} v\ dx - f^{s}v(1) \quad \forall x \in ]0,1[ \\
u(0) &= 0 \\
\forall v \text{ with } v(0) &= 0
\end{align}
$$
Governing PDE in *weak form* (weak: not pointwise, only over the entire integral).

Requires *only* first derivatives of $u$.
#### Derivation
Assume strong form is satisfied: $E \partial_{xx} u(x) + f^{b}(x) = 0$ for all $x \in ]0,1[$.

Idea: For a sufficiently smooth function $v(x),\ v(0) = 0$, we have:
$$
\int^{1}_{0}\left( E \partial_{xx} u(x) + f^{b}(x) \right) \cdot v(x) dx = 0
$$
(since the left term is always 0, the $v(x)$ doesn't matter)

Why? Transfer one level of integration from $u$ to $v$ via integration by parts ($\int^{1}_{0} f'g = [fg]_{0}^{1} - \int^{1}_{0}fg'$):
$$
\begin{align}
-\int^{1}_{0} E \partial_{x} u\ \partial_{x}v\ dx + [E\partial_{x} u \cdot v]_{0}^{1} + \int^{1}_{0} f^{b} v\ dx &= 0 \\
\Rightarrow -\int^{1}_{0} E \partial_{x} u\ \partial_{x}v\ dx -f^{s}v(1) + \int^{1}_{0} f^{b} v\ dx &= 0 \\
\text{Because: } v(0) = 0, E\partial_{x} u(1) = -f^{s}
\end{align}
$$
## Solving it
[[Discrete Energy Approach]], but skipped in lecture.
