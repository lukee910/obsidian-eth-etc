Like a [[BRDF]] for scattering in [[Participating Media]].

Note: Integrates to unity (unlike the BRDF):
$$
\int_{S^{2}} f_{p}(x, \vec{\omega}', \vec{\omega})\ d \vec{\omega}' = 1
$$
## Common Phase Functions
### Isotropic Scattering
Uniform scattering, analog of diffuse BRDF.
#TODO: Formula
### Henyey-Greenstein Phase Function
Empirical phase function. Anisotropic.

$$
f_{p \text{ HG}}(\theta) = \frac{1}{4\pi} \frac{1 - g^{2}}{(1 + g^{2} - 2g \cos\theta)^{\frac{3}{2}}}
$$

Recommendation: If you have a lot of noise in your volume, check that you're not above 0.8 for $g$ (then stuff gets freaky).
#### Sampling
#TODO: Slides 16 slide 74 sampling function
## Sampling
Get an angle proportional to the phase function, to do scattering within a volume. Equivalent to BRDF.