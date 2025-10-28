## Recap
Bright outliers: The rare BRDF samples that hit the light via reflection.
## Early Termination of Rays
Truncating at some fixed point introduces bias.

Solution: [[#Russian Roulette]]
## Russian Roulette
- Probabilistically terminate the recursion
- Choose continuation probability $q \in (0,1)$
- Generate random number $\xi$
- #TODO: Result

$q$ is usually decided based on [[#Path Throughput Weight]].
### Properties
- *Always* increases sample variance
- *Always* reduces time per sample
- *Can* improve efficiency
	- Early terminate paths with small contributions
### Path Throughput Weight
$$
\beta = \prod_{j=1}^{i-2}\frac{f(x_{j}, x_{j+1}, x_{j-1}) |\cos(\theta_{j})|}{p_{\omega}(x_{j+1} - x_{j})}
$$
Nominator: Path throughput up to bounce $i$. Denominator: Pdf product up to bounce $i$. 
## Path Tracing
#TODO: Slide 39, how it is composed in code
#TODO: Add "Next Event Estimation" to terminology

Note ray tracing vs path tracing: Ray tracing loses throughput, as ray counts explode. For path tracing, we just continue one ray across it, *constant number* of paths. Add [[#Russian Roulette]] and we have a *decreasing number* of paths.
### Progressive Path Tracing
Alternative way of writing path tracing. Difference is only about user feedback.

"Normal" path tracing is "Blocked": Calculates blocks in a go. Can only see the result when the block is done for all samples.

Progressive: Progressively samples better over all the pixels. Image is built up progressively as it is rendered.
### Path Tracing Caustics
Really hard, because Next Event Estimation doesn't work. Have to gamba that the BRDF bounces hit.

Can we do this better? See [[#Duality of Radiance and Importance]]
## Duality of Radiance and Importance
### Measurement Equation
Rendering equation describes radiative equilibrium at point $x$: #TODO
$$
L_{o}(x, \vec{\omega}_{o}) = L_{e}(x, \vec{\omega}_{o}) + \int_{H^{2}} f_{r}(x, \vec{\omega}_{i}, \vec{\omega}_{o}) L_{i}(x, \vec{\omega}_{i}) \cos \theta_{i}\ d \vec{\omega}_{i}
$$

We are interested in the total radiance contributing to *pixel $j$:*
$$
I_{j}=\int_{A_{film}} \int_{H^{2}} W_{e}(x, \vec{\omega}) L_{i}(x, \vec{\omega}) \cos \theta\ d\vec{\omega}\ dx
$$
### Radiance vs Importance
- Radiance
	- Emitted from light sources
	- Describes amount of light traveling within a differential beam
- Importance
	- Emitted from sensors
	- Describes the response of the sensor to radiance travelling within a differential beam

#TODO: Slide 61 ff formulas making the equivalence $I_{j} \to L_{o}$.

Idea from this: [[#Light Tracing]]
## Light Tracing
- Shoot multiple paths from light sources
- Search/Query for importance
- Connect to the image using NEE (ask if we can connect to camera, equivalent to shadow rays in PT)
### Light Tracing Caustics
[[#Path Tracing Caustics]]

Becomes much easier, since we can connect to the camera *after* the caustic intersection.

However: Symmetric issue with caustics between the camera and intersection point. Caustics will be black, since the camera is basically a point light.

