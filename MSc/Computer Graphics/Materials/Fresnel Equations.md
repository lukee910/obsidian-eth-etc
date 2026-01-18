---
~
---
## Idea
Model the refraction and reflection ratio for [[Dielectric Material]]s and [[Conductor Material]]s. Derived from Maxwell equations.

![[Fresnel Equations Setup.png]]
## Dielectrics
[[Dielectric Material]]
$$
\begin{align}
\rho_{||} &= \frac{\eta_{2} \cos \theta_{1} - \eta_{1}\cos \theta_{2}}{\eta_{2} \cos \theta_{1} + \eta_{1} \cos \theta_{2}} \\
\rho_{\perp} &= \frac{\eta_{1} \cos \theta_{1} - \eta_{2}\cos \theta_{2}}{\eta_{1} \cos \theta_{1} + \eta_{2} \cos \theta_{2}}
\end{align}
$$
Reflected:
$$
F_{r} = \frac{1}{2} \left( \rho_{||}^{2} + \rho_{\perp}^{2} \right)
$$
Refracted:
$$
F_{t} = 1 - F_r
$$

Note: Faster approximations available (e.g. [Schlick](https://en.wikipedia.org/wiki/Schlick%27s_approximation)).
## Conductors
[[Conductor Material]]
$$
\begin{align}
\rho_{||}^{2} &= \frac{(\eta^{2} + k^{2}) \cos^{2} \theta_{i} - 2\eta \cos \theta_{i} + 1}{(\eta^{2} + k^{2}) \cos^{2} \theta_{i} + 2\eta \cos \theta_{i} + 1} \\
\rho_{\perp}^{2} &= \frac{(\eta^{2} + k^{2}) - 2\eta \cos \theta_{i} + \cos^{2} \theta_{i}}{(\eta^{2} + k^{2}) + 2\eta \cos \theta_{i} + \cos^{2} \theta_{i}}
\end{align}
$$
With:
- $\eta$ Index of refraction
- $k$ Absorption coefficient
- NOTE: $\eta$ and $k$ are wavelength dependent!

Reflected: (same as [[#Dielectrics]])
$$
F_{r} = \frac{1}{2} \left( \rho_{||}^{2} + \rho_{\perp}^{2} \right)
$$
Note: Other light is absorbed instead.
