Part of the [[Rendering Equation]].
## Definition
$$
L_{r}(x, \vec{\omega}_{r}) = \int_{H^{2}} f_{r}(x, \vec{\omega}_{i}, \vec{\omega}_{r}) L_{i}(r(x, \vec{\omega}_{i}), -\vec{\omega}_{i}) \cos \theta_{i}\ d \vec{\omega}_{i}
$$
## Integration Forms
### Converting Between Forms
#### Notation
- $L_{i}(x, \vec{\omega}_{i}) = L_{i}(x, y)$
- $L_{r}(x, \vec{\omega}_{i}) = L_{r}(x, z)$
- $f_{r}(x, \vec{\omega}_{i}, \vec{\omega}_{r}) = f_{r}(x, y, z)$
For:
![[Reflection Equation Forms Notation.png|200]]
#### Jacobian Determinant
$$
d \vec{\omega}_{i} = \frac{|\cos \theta_{o}|}{\|x-y\|^{2}}\ dA
$$
![[Jacobian of Reflection Transformation.png|200]]
Via [[Solid Angle#Formulas]] $d\vec{\omega}_{i}$ and $dA$ relation: $d\overrightarrow{\omega} = \frac{dA}{r^{2}} = \sin(\theta)\ d\theta\ d\phi$, and getting the determinant.

See also: [PBR 2.4.1 Transformation in Multiple Dimensions](https://www.pbr-book.org/4ed/Monte_Carlo_Integration/Transforming_between_Distributions#TransformationinMultipleDimensions)
### Hemispherical Integration
![[#Definition]]
![[Reflection Equation Hemispherical Integration.png|400]]
### Surface Area Integration
$$
L_{r}(x, z) = \int_{A} f_{r}(x, y, z) L_{i}(x, y) G(x, y)\ dA(y)
$$
With geometry term $G(x, y)$:
$$
G(x, y) = V(x, y) \frac{|\cos \theta_{i}||\cos \theta_{o}|}{\| x - y \|^{2}}
$$
And visibility term $V(x, y)$:
$$
V(x, y) = \begin{cases}
1 & \text{visible} \\
2 & \text{not visible}
\end{cases}
$$
![[Reflection Equation Surface Area Integration.png|400]]
Note:
- In $G$:
	- $\cos \theta_{i}$: Foreshortening term from basic [[#Definition]]
	- $\frac{|\cos \theta_{o}|}{\|x-y|\|^{2}}$: [[#Jacobian Determinant]]
- Interpreting $\frac{|\cos \theta_{i}||\cos \theta_{o}|}{\| x - y \|^{2}}$:
  ![[Reflection Equation Cosine Terms.png|300]]
	- The chance that a photon emitted from a differential patch will hit another differential patch decreases as:
		- The patches face away (numerator)
		- The patches move away (denominator)
## Direct Illumination
Applying the [[#Surface Area Integration]] formulation to [[Direct Illumination]]:
![[Reflection Eq Direct Illumination.png|600]]
## Importance Sampling
[[Reflection Equation Importance Sampling]]
