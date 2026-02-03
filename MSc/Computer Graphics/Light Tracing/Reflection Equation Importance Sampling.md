Idea: Apply [[Importance Sampling]] to various terms of the [[Reflection Equation]].
## Cosine Term
Apply to the $\cos \theta_{i}$ term.

See: [[Ambient Occlusion#Monte Carlo Implementation]]
## BRDF Term
Idea: BRDF (especially those with a large [[Ideal Specular BSDFs]] component) are not simply cosine weighted:
![[Importance Sampling BRDF.png]]
### Recipe
1. Find a convenient coordinate frame for drawing samples from the desired distribution
	1. Compute the [[Jacobian]] of the transform between the sampling frame and the frame where you integrate
2. Compute marginal and conditional 1D PDFs
3. Sample 1D PDFs using the [[CG 04V2 Monte Carlo#Inversion Method Process]].
### BRDFs with multiple Lobes
Typically, each lobe has a scaling coefficient, e.g. $k_{d}$ for diffuse and $k_{s}$ for specular.

1. Probabilistically choose a lobe, e.g. proportional to the coefficient
2. Sample a direction using the lobe: $$ p_{\Omega}(\omega) = p_{l}(l)p_{\Omega}(\omega | l) $$
With:
- $p_{l}(l)$: Probability of sampling that lobe
- $p_{\Omega}(\omega)$: Probability of sampling that direction
### Example: Normalized Phong
![[Normalized Phong Importance Sample.png]]
### Example: Microfacet Models
- Sample the distribution to get a microfacet normal
- Reflect the incident direction about the normal
![[Microfacet Importance Sample.png]]
## Importance Sampling Incident Radiance
Impossible in general, but possible for [[Direct Illumination]]. Do this by directly sampling the emissive surface.
