## St. Venant Kirchhoff Material (StVK)
First idea: Replace Cauchy strain with Green strain in [[Linear Elasticity Model]].

Energy density: $\Psi = \frac{1}{2} \lambda\ tr(E)^{2} + \mu\ tr(E^{2})$ 

Problem: Is a fourth order function, has multiple local minima!
![[StVK Local Minima.png]]
0 Volume can be achieved with finite energy. When reaching 0.5 times the deformation, the material collapses.

**NOTE: Nobody uses this in practice!**
## Neo-Hookean Material
Strain energy density for a compressible Neo-Hookean solid is defined as:
$$
\Psi_{NH} = \frac{\mu}{2}(tr(C) - 3) - \gamma \ln(J) + \frac{\mu}{2} \ln(J)^{2}
$$
With:
* $C = |F|^{2}_{F}$
* $J = \det F$

Note:
* First term penalizes all deformations equally (same as [[Linear Elasticity Model]])
* Second and third terms to go infinity for increasing compression
	* Cannot invert material with finite energy!
* Problem: Logs can be a headache, Newton's Method can run into negative numbers (which can't be used in a $\ln$)

Can be used for rubber-like materials with deformations of up to 20%.
