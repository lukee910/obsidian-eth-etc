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
Where $\sigma_{a}(x)$ is the (spatially varying) [[Absorption Coefficient]], unit is $[m^{-1}]$, radiance absorbed per unit difference. $\sigma_{a} \in [0, \infty[$. Can also be *spectrally* variant, e.g. absorb more blue or green light etc.
### Out-Scattering
$$
dL(x, \vec{\omega}) = -\sigma_{s}(x)L(x, \vec{\omega}) dz
$$
Where $\sigma_{s}(x)$ is the (spatially, spectrally varying) [[Scattering Coefficient]], unit is $[m^{-1}]$, $\sigma_{s} \in [0, \infty[$.
### In-Scattering
$$
dL(x, \vec{\omega}) = \sigma_{s}(x)L_{s}(x, \vec{\omega}) dz
$$
Note:
- $\sigma_{s}$ without the $-$ in front.
- $L_{s}(x, \vec{\omega})$: In-scattered radiance
- [[Scattering Coefficient]]
### Emission
$$
dL(x, \vec{\omega}) = \sigma_{a}(x)L_{e}(x, \vec{\omega}) dz
$$
Note:
- $L_{e}(x, \vec{\omega})$ emitted radiance.
- Convention: Multiply with absorption coefficient. Idea: There has to be some medium that emits this radiance. Have to pay attention if this is done or not!
- [[Absorption Coefficient]]
## Radiative Transport Equation
$$
\begin{align}
dL(x, \vec{\omega}) = &-\sigma_{a}(x)L(x, \vec{\omega}) dz \\
&-\sigma_{s}(x)L(x, \vec{\omega}) dz \\
&+ \sigma_{a}(x)L_{e}(x, \vec{\omega}) dz \\
&+ \sigma_{s}(x)L_{s}(x, \vec{\omega}) dz
\end{align}
$$
- Negative terms: Losses ([[#Absorption]], [[#Out-Scattering]])
- Positive terms: Gains ([[#Emission]], [[#In-Scattering]])
- Based on [[Absorption Coefficient]] and [[Scattering Coefficient]].
## Losses
Combines [[#Absorption]] and [[#Out-Scattering]]:
$$
\begin{align}
dL(x, \vec{\omega}) &= -\sigma_{a}(x)L(x, \vec{\omega}) dz -\sigma_{s}(x)L(x, \vec{\omega}) dz \\
&= -\sigma_{t}(x) L(x, \vec{\omega}) dz
\end{align}
$$
With [[Extinction Coefficient|Extinction Coefficient ($\sigma_t$)]]
## Transmittance
[[Transmittance]]