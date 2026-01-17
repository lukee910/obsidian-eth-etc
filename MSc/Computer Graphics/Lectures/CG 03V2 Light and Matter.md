## Light
[[_T Light, Radiometry]]
### Intro
(Intro: Wave Theory vs Corpuscular Theory)
### Blackbody
[[Blackbody]]
### Light Emission
[[Types of Light Emission]]
### Radiometry
#### Basic quantities
[[Radiometric Quantities]]
#### Irradiance vs Radiance
With:
[[Irradiance]]: $E(x)$
[[Radiance]]: $L(x, \vec{\omega})$
[[Flux]]: $\Phi(A)$
$$
E(x) = \frac{d\Phi(A)}{dA(x)}
$$

We get the equivalence:
$$
\begin{align}
L(x, \vec{\omega}) &= \frac{d^{2} \Phi(A)}{\cos(\theta)\ dA(x)\ d\vec{w}}
\\
L(x, \vec{\omega}) &= \frac{d E(x)}{\cos(\theta)\ d\vec{w}} \quad (\text{Insert } E(x)) \\
L(x, \vec{\omega}) \cos \theta\ d \vec{\omega} &= dE(x) \\
\int_{H^{2}} L(x, \vec{\omega}) \cos \theta\ d \vec{\omega} &= E(x)
\end{align}
$$
## Material
[[_T Materials]]
### BRDF vs BTDF, reflection vs refraction
[[BRDF]]
- BRDF: Reflection
- BTDF: Refraction, medium transfer
	- Example: [[BRDF#BTDF of Ideal Specular Refraction]]
### Example BRDFs, BTDFs
[[Ideal Specular BSDFs]]
### Fresnel Equations
[[Fresnel Equations]]
### Total Internal Reflection
#TODO
