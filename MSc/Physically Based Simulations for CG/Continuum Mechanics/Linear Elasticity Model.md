Material model links strain to stress (and energy)

For [[Hyperelastic Material]]s, stress derives directly from postulated energy density $\Psi$.
## Isotropic Material
When the same stretch is applied in two different directions, you get the same forces (corresponding by rotation).
## Linear Isotropic Material
(generalized Hooke's law)

Energy density: $\Psi = \frac{1}{2} \lambda\ tr(\varepsilon)^{2} + \mu\ tr(\varepsilon^{2})$ ($\varepsilon$ [[3D Non-Linear Strain#Cauchy Strain|Cauchy Strain]], matrix; $\lambda,\gamma$ Lamé parameters, scalar)

Cauchy Stress: $\sigma = \frac{\partial \Psi}{\partial \varepsilon} = \lambda\ tr(\varepsilon) I + 2 \gamma \varepsilon$.

Interpretation: $tr(\varepsilon^{2})$ penalizes all strain components equally. $\lambda\ tr(\varepsilon)^{2}$ penalizes dilatations, i.e. volume changes. Traces approximates the determinant of the volume change, but is linear so easier to compute.

For material parameters, check the [Lamé Parameters on Wikipedia](https://en.wikipedia.org/wiki/Lam%C3%A9_parameters).
## Limitations
Uses Cauchy strain, so is not invariant under rotations.

Solution: Use nonlinear deformation measure $\to$ nonlinear elasticity.