## Sampling Based on Terms
Idea: Apply [[Importance Sampling]] to various terms of the [[Reflection Equation]].
### Cosine Term
Apply to the $\cos \theta_{i}$ term.

See: [[Ambient Occlusion#Monte Carlo Implementation]]
### BRDF Term
Idea: BRDF (especially those with a large [[Ideal Specular BSDFs]] component) are not simply cosine weighted:
![[Importance Sampling BRDF.png]]
Note: I think in [[Nori]] this is the Mats component.
#### Recipe
1. Find a convenient coordinate frame for drawing samples from the desired distribution
	1. Compute the [[Jacobian]] of the transform between the sampling frame and the frame where you integrate
2. Compute marginal and conditional 1D PDFs
3. Sample 1D PDFs using the [[CG 04V2 Monte Carlo#Inversion Method Process]].
#### BRDFs with multiple Lobes
Typically, each lobe has a scaling coefficient, e.g. $k_{d}$ for diffuse and $k_{s}$ for specular.

1. Probabilistically choose a lobe, e.g. proportional to the coefficient
2. Sample a direction using the lobe: $$ p_{\Omega}(\omega) = p_{l}(l)p_{\Omega}(\omega | l) $$
With:
- $p_{l}(l)$: Probability of sampling that lobe
- $p_{\Omega}(\omega)$: Probability of sampling that direction
#### Example: Normalized Phong
![[Normalized Phong Importance Sample.png]]
#### Example: Microfacet Models
- Sample the distribution to get a microfacet normal
- Reflect the incident direction about the normal
![[Microfacet Importance Sample.png]]
### Importance Sampling Incident Radiance
Impossible in general, but possible for [[Direct Illumination]]. Do this by directly sampling the emissive surface.

Note: In [Nori], this is emitter sampling.
## Mixed Importance Sampling
Idea: Mix two sampling strategies, "best of both worlds". Simplified version of [[Multiple Importance Sampling]].

Motivation:
![[Importance Sampling Multiple Strategies.png]]
#### Mixed - Cosine Contribution
[[#Cosine Term]], "Cosine-Weighted Hemisphere" in picture above.

[[Reflection Equation#Hemispherical Integration]] form:
$$
L_{r}(x, \vec{\omega}_{r}) = \int_{H^{2}} f_{r}(x, \vec{\omega}_{i}, \vec{\omega}_{r}) L_{e}\left(r(x, \vec{\omega}_{i}), -\vec{\omega}_{i}\right) \cos \theta_{i}\ d\vec{\omega}_{i}
$$

[[Probability Density Function|PDF]]:
$$
p_{1}(\vec{\omega}) = \frac{\cos \theta}{\pi}
$$
#### Mixed - Incident Radiance Contribution
[[#Importance Sampling Incident Radiance]], "Uniform Surface Area" in picture above.

[[Reflection Equation#Surface Area Integration]] form:
$$
L_{r}(x, z) = \int_{A} f_{r}(x, y, z) L_{e}(y, x) V(x, y) \frac{|\cos \theta_{i}||cos \theta_{o}|}{\| x- y \|^{2}}\ dA(y)
$$
[[Probability Density Function|PDF]]:
$$
\begin{align}
p_{2}(x) &= \frac{1}{A} \\
&= \frac{1}{A} \frac{d^{2}}{\cos \theta}
\end{align}
$$
#Unclear Which $\theta$?
#### Combining Contributions
Idea: Sample from the average PDF:
$$
\frac{1}{N} \sum\limits_{i=1}^{N} \frac{f(x_{i})}{0.5(p_{1}(x_{i}) + p_{2}(x_{i}))}
$$
This says "How likely is this ray on average over both measures?"

The following _does not_ reduce [[Variance]], since Variance is additive (but shows the picture a bit simpler):
$$
\frac{0.5}{N_{1}} \sum\limits_{i=1}^{N_{1}}\frac{f(x_{i})}{p_{1}(x_{i})} + \frac{0.5}{N_{2}} \sum\limits_{i=1}^{N_{2}}\frac{f(x_{i})}{p_{2}(x_{i})}
$$

Getting the probabilities:
### Mixed Importance Sampling vs Multiple Importance Sampling
[[Multiple Importance Sampling]]

