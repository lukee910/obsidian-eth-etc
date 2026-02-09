## Recap
[[BRDF]]
Lambertian Reflection, Perfect Reflection
## Fresnel Equations for Conductors
![[Fresnel Equations#Conductors]]
## Specular BSDF
![[Ideal Specular BSDFs]]
## Rendering with Delta BRDFs
Use the delta function properties to not fully solve the integral over the hemisphere. Specular directions are solved explicitly via the Dirac delta, only reflected from one direction.

## Polarization
Idk what the point of this part was, #Unclear?
## Advanced Models
Rough conductors and dielectrics.
Idea: Micro scale is not smooth for a flat surface, has some roughness.
### Empirical Models
Empirical, Glossy.
#### Phong
Empirical model via cosine blurring based on specular reflection direction $\vec{\omega}_{r}$. Concretely, exponentiated cosine lobe:
$$
\begin{align}
f_{r}(\vec{\omega_{o}}, \vec{\omega_{i}}) &= \frac{e+2}{2\pi}(\vec{\omega_{r}} \cdot \vec{\omega_{o}})^{e} \\
\vec{\omega_{r}} &= (2\vec{n}(\vec{n} \cdot \vec{\omega_{i}}) - \vec{\omega_{i}})
\end{align}
$$
Interpretation: Blur reflection rays in a cone about the mirror direction.
#### Blinn-Phong
Blur in normal domain instead of the reflection direction.
$$
\begin{align}
f_{r}(\vec{\omega_{o}}, \vec{\omega_{i}}) &= \frac{e+2}{2\pi}(\vec{\omega_{h}} \cdot \vec{n})^{e} \\
\vec{\omega_{h}} &= \frac{\vec{\omega}_{i} + \vec{\omega}_{o}}{\| \vec{\omega}_{i} + \vec{\omega}_{o} \|}
\end{align}
$$
#### Empirical Limitations
- Not physically based
- (Often) not reciprocal
	- #Unclear
- Not energy-preserving
- No [[Fresnel Equations|Fresnel]] effects
- Limited surfaces they can model
- May generate directions below the surface
=> [[#Microfacet Theory]]
### Microfacet Theory
[[_T Microfacets]]
Explains off-specular peaks (that look specular).

Assumes surface is composed of many micro-grooves, each of which is perfectly flat. Each facet is perfectly specular.

#### General Microfacet Model
$$
f_{r}(\vec{\omega_{o}}, \vec{\omega_{i}}) = \frac{F(\vec{\omega_{h}}, \vec{\omega_{o}}) \cdot D(\vec{\omega_{h}}) \cdot G(\vec{\omega_{o}}, \vec{\omega_{i}})}{4|(\vec{\omega_{i}} \cdot \vec{n})(\vec{\omega_{o}} \cdot \vec{n})|}
$$
$F(\vec{\omega_{o}}, \vec{\omega_{i}})$: Fresnel Coefficient
$D(\vec{\omega_{h}})$: Microfacet Distribution
$G(\vec{\omega_{o}}, \vec{\omega_{i}})$: Shadowing/Masking

##### Fresnel Term
Reflection at certain angles
[[Fresnel Equations]]
##### Microfacet Distribution
What fraction of microfacets face each direction? $\to$ probability density function.

$$
\int_{H^{2}} D(\vec{\omega_{h}}) \cos(\theta_{h}) d\vec{\omega_{h}} = 1
$$
Normalized over the hemisphere, over the **projected** solid angle (outgoing direction).
###### The Beckmann Distribution
The slopes follow a Gaussian distribution.
$$
D(\vec{\omega}_{h}) = \frac{1}{\pi \alpha^{2}\cos^{4}\theta_{h}} e^{-\frac{\tan^{2}\theta_{h}}{\alpha^{2}}}
$$

($e^{-\frac{\tan^{2}\theta_{h}}{\alpha^{2}}}$ is the distribution, the rest is just to make it integrate to 1)

Note:
- $\alpha$ is the standard deviation of the surface slope
	- The larger the $\alpha$, the rougher the surface and the wider the spread
	- $\alpha = 0$ is mirror-like
- Slope of a surface with $\theta_{h}$ is $\tan \theta_{h}$
###### Blinn Distribution
$$
D(\vec{\omega}_{h}) = \frac{e + 2}{2 \pi}(\vec{\omega}_{h} \cdot \vec{n})^{e}
$$
###### GGX Distribution
See [Walter et al., EGSR 2007](https://dl.acm.org/citation.cfm?id=2383874).
##### Shadowing / Masking
Idea: Microfacets may be shadowed by other microfacets.

Introduce a term $G(\vec{\omega}_{i}, \vec{\omega}_{o})$:
$$
f(\vec{\omega}_{i}, \vec{\omega}_{o}) = \frac{F(\vec{\omega}_{h}, \vec{\omega}_{o}) \cdot D(\vec{\omega}_{h}) \cdot \mathbf{G(\vec{\omega}_{i}, \vec{\omega}_{o})}}{4 |(\vec{\omega}_{i} \cdot \vec{n}) (\vec{\omega}_{o}\cdot \vec{n})|}
$$
###### Beckmann Shadowing
Using:
$$
\begin{align}
s &= \frac{1}{\alpha \tan \theta} \\
G(\vec{\omega}) &= \frac{2}{1 + \text{erf}(s) + \frac{1}{s\sqrt{\pi}} e^{-s^{2}}} & \text{exact} \\
G(\vec{\omega}) &= \begin{cases}
\frac{3.535 s + 2.181 s^{2}}{1 + 2.276s + 2.577 s^{2}}, & s < 1.6 \\ \\
1, &\text{else}
\end{cases} & \text{approximate}
\end{align}
$$
We get:
$$
G(\vec{\omega}_{i}, \vec{\omega}_{o}) = G(\vec{\omega}_{i}) \cdot G(\vec{\omega}_{o})
$$
###### Torrance-Sparrow Shadowing (Blinn)
$$
G(\vec{\omega}_{i}, \vec{\omega}_{o}) = \min \left( 1, \frac{2 (\vec{n} \cdot \vec{\omega}_{h})(\vec{n} \cdot \vec{\omega}_{i})}{\vec{\omega}_{h} \cdot \vec{\omega}_{i}}, \frac{2 (\vec{n} \cdot \vec{\omega}_{h})(\vec{n} \cdot \vec{\omega}_{o})}{\vec{\omega}_{h} \cdot \vec{\omega}_{o}} \right)
$$
#### Sampling the Microfacet Model
Idea: Start by sampling $\vec{\omega_{h}}$ with PDF proportional to D, because that's the most problematic one.
#### Layered Surface
Note: When adding a coating, you have to account for intra-layer reflections and refractions.
### Oren-Nayar Model
Same concept as the microfacets, but assumes the facets are **diffuse**.

No analytic solution, fitted approximation exists.
### Data-Driven BRDFs
e.g.:
* [http://www.merl.com/brdf/]
* [http://rgl.epfl.ch/materials]
