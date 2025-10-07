## Recap
[[BRDF]]
Lambertian Reflection, Perfect Reflection
## Fresnel Equations for Conductors
vs [[CG 03V2 Light and Matter#Fresnel Equations]].
#TODO: This.

## BRDF of Specular Reflection
#TODO: In [[BRDF#BRDF of Ideal Specular Reflection]]
## BTDF of Specular Refraction
#TODO: Formula

For refraction, the hemisphere will be compressed into a cone in the medium, represented by $\frac{\eta_{1}^{2}}{\eta_{2}^{2}}$.
## Rendering with Delta BRDFs
Use the delta function properties to not fully solve the integral over the hemisphere. Specular directions are solved explicitly via the Dirac delta, only reflected from one direction.

## Polarization
idk what the point of this part was, #TODO?

## Advanced Models
Rough conductors and dielectrics.
Idea: Microscale is not smooth for a flat surface, has some roughness.
### Empirical Models
#### Phong
Empirical model via cosine blurring. Concretely, exponentiated cosine lobe:
$$
\begin{align}
f_{r}(\vec{\omega_{o}}, \vec{\omega_{i}}) &= \frac{e+2}{2\pi}(\vec{\omega_{r}} \cdot \vec{\omega_{o}})^{e} \\
\vec{\omega_{r}} &= (2\vec{n}(\vec{n} \cdot \vec{\omega_{i}}) - \vec{\omega_{i}})
\end{align}
$$
Interpretation: Blur reflection rays in a cone about the mirror direction.
#### Blinn-Phong
Blur in normal domain instead of the reflection directions.
$$
\begin{align}
f_{r}(\vec{\omega_{o}}, \vec{\omega_{i}}) &= \frac{e+2}{2\pi}(\vec{\omega_{h}} \cdot \vec{n})^{e} \\
\vec{\omega_{h}} &= \text{\#TODO} \text{half-way vector}
\end{align}
$$
#TODO: This
#### Empirical Limitations
#TODO 
### Microfacet Theory
[[_T Microfacets]]
Explains off-specular peaks (that look specular).

Assumes surface is composed of many micro-grooves, each of which is perfectly flat. Each facet can be specular or diffuse.

#### General Microfacet Model
$$
f_{r}(\vec{\omega_{o}}, \vec{\omega_{i}}) = \frac{F(\vec{\omega_{h}}, \vec{\omega_{o}}) \cdot D(\vec{\omega_{h}}) \cdot G(\vec{\omega_{o}}, \vec{\omega_{i}})}{4|(\vec{\omega_{i}} \cdot \vec{n})(\vec{\omega_{o}} \cdot \vec{n})|}
$$
$F(\vec{\omega_{o}}, \vec{\omega_{i}})$: Fresnel Coefficient
$D(\vec{\omega_{h}})$: Microfacet Distribution
$G(\vec{\omega_{o}}, \vec{\omega_{i}})$: Shadowing/Masking

##### Fresnel Term
Reflection at certain angles
#TODO: Link to other Fresnel theory
##### Microfacet Distribution
What fraction of microfacets face each direction? $\to$ probability density function.

$$
\int_{H^{2}} D(\vec{\omega_{h}}) \cos(\theta_{h}) d\vec{\omega_{h}} = 1
$$
Normalized over the hemisphere, over the **projected** solid angle (outgoing direction).
###### The Beckmann Distribution
The slopes follow a Gaussian distribution.
#TODO: Formula
($e^{-smth}$ is the distribution, the rest is just to make it integrate to 1)
###### Blinn Distribution
#TODO: Formula
###### GGX Distribution
#TODO: Formula
##### Shadowing / Masking
Idea: Microfacets may be shadowed by other microfacets.

#TODO: Formula for Beckmann.

#TODO: Formula for Torrance-Sparrow (Blinn Distribution)
#### Sampling the Microfacet Model
Idea: Start by sampling $\vec{\omega_{h}}$ with PDF proportional to D, because that's the most problematic one.


