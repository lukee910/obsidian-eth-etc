Setup: Diffuse objects illuminated by an ambient white sky.

[[Reflection Equation]] simplifies to:
$$
L_{r}(x) = \frac{\rho}{\pi} \int_{H^{2}} V(x, \vec{\omega}_{i}) \cos \theta_{i}\ d \vec{\omega}_{i}
$$
Idea: [[Direct Illumination]] setup. Integrate over the hemisphere, see if we reach the sky $V(x, \vec{\omega}_{i})$. $f_{r} = 1$, $L_{e} = 1$, $\rho$ controls the [[Flux|Radiant Power]] total.
## Monte Carlo Implementation
[[Monte Carlo Estimator]]
![[Ambient Occlusion Monte Carlo.png]]
Resulting in an improvement in [[Variance]]: (Note that the two versions converge, look very similar at ~1024 spp)
![[Ambient Occlusion Sampling Result.png]]
