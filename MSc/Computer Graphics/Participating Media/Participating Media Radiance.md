## Radiance
[[Radiance]] changes along the ray:
$$
L_{i}(x, \vec{\omega}) \neq L_{o}(r(x, \vec{\omega}), -\vec{\omega})
$$
We'll work on a [[Differential Beam#Segment]].
### Absorption
$$
dL(x, \vec{\omega}) = -\sigma_{a}(x)L(x, \vec{\omega}) dz
$$
Where $\sigma_{a}(x)$ is the (spatially varying) absorption coefficient, unit is $[m^{-1}]$, radiance absorbed per unit difference. $\sigma_{a} \in [0, \infty[$. Can also be *spectrally* variant, e.g. absorb more blue or green etc.
### Out-Scattering
$$
dL(x, \vec{\omega}) = -\sigma_{s}(x)L(x, \vec{\omega}) dz
$$
Where $\sigma_{s}(x)$ is the (spatially, spectrally varying) scattering coefficient, unit is $[m^{-1}]$, $\sigma_{s} \in [0, \infty[$.
### In-Scattering
$$
dL(x, \vec{\omega}) = \sigma_{s}(x)L_{s}(x, \vec{\omega}) dz
$$
Note:
- $\sigma_{s}$ without the $-$ in front.
- $L_{s}(x, \vec{\omega})$: In-scattered radiance
### Emission
$$
dL(x, \vec{\omega}) = \sigma_{a}(x)L_{e}(x, \vec{\omega}) dz
$$
Note:
- $L_{e}(x, \vec{\omega})$ emitted radiance.
- Convention: Multiply with absorption coefficient. Idea: There has to be some medium that emits this radiance. Have to pay attention if this is done or not!
## Radiative Transport Equation
$$
\begin{align}
dL(x, \vec{\omega}) = &-\sigma_{a}(x)L(x, \vec{\omega}) dz \\
&-\sigma_{s}(x)L(x, \vec{\omega}) dz \\
&+ \sigma_{a}(x)L_{e}(x, \vec{\omega}) dz \\
&+ \sigma_{s}(x)L_{s}(x, \vec{\omega}) dz
\end{align}
$$
## Losses (Extinction Coefficient)
[[#Absorption]] + [[#Out-Scattering]] simplifications.
#TODO: This formula and $\sigma_{t}$
## Beer-Lambert Law - Extinction along a finite beam
#TODO: Derivation slide 31
$$
\frac{L_{z}}{L_{0}} = e^{-\sigma_{t}z}
$$
This fraction is the [[#Transmittance]].
## Transmittance
### Transmittance Homogenous Volume
$$
T_{r}(x, y) = e^{-\sigma_{t}\|x-y\|}
$$
### Transmittance in Heterogeneous Volumes
$$
T_{r}(x, y) = e^{-\int_{0}^{\|x-y\|} \sigma_{t}(t)\ dt}
$$
### Transmittance Multiplicativity
$T_{r}(x,z) = T_{r}(x,y) T_{r}(y,z)$
For $x,y,z$ in this order along a beam.
