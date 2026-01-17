[[BRDF]]
## BRDF of Ideal Specular Reflection
$$
f_{r}(x, \vec{\omega_{i}}, \vec{\omega_{r}}) = F_{r}(\vec{\omega_{i}}) \frac{\delta \left( \vec{\omega}_{r} - R(\vec{\omega}_{i}, \vec{n}) \right)}{\cos \theta_{i}}
$$
- $F_{r}$ Fresnel reflection
- $\delta$ Dirac delta
	- Integral issues!
- $R$ Reflection function
	- R flips the mirrors vector by the normal, defines the direction change.
- $\delta(...)$ is $1$ if and only if the reflected direction $\vec{\omega}_{r}$ is exactly the reflection calculated by $R$.
- $\cos \theta_{i}$ cancels the cosine term in the reflection equation ( #Unclear where exactly?)
## BTDF of Ideal Specular Refraction
(Bidirectional Transmittance Distribution Function)

$$
f_{r}(x, \vec{\omega_{i}}, \vec{\omega_{r}}) = \frac{\eta_{1}^{2}}{\eta_{2}^{2}} (1 - F_{r}(\vec{\omega_{i}})) \frac{\delta \left( \vec{\omega}_{r} - T(\vec{\omega}_{i}, \vec{n}) \right)}{\cos \theta_{i}}
$$

Where:
- $T$ Transmittance function just returns straight through the material.
- $\frac{\eta_{1}^{2}}{\eta_{2}^{2}}$ determines the bending of the light, where the light is directed to
	- A hemisphere will be compressed into a $\pi \cdot \frac{\eta_{1}^{2}}{\eta_{2}^{2}}$ sized cone.
