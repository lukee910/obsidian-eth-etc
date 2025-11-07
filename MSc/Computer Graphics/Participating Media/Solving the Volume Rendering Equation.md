[[Volume Rendering Equation]]
## In-Scattered Radiance
$$
L(x, \vec{\omega}) = \int^{z}_{0} T_{r}(x, x_{t}) \sigma_{s}(x_{t}) L_{s}(x_{t}, \vec{\omega})\ dt
$$
We look at:
$$
L_{s}(x_{t}, \vec{\omega}) = \int_{S^{2}} f_{p}(x_{t}, \vec{\omega}', \vec{\omega}) L_{i}(x_{t}, \vec{\omega}')\ d \vec{\omega}'
$$
### Single Scattering
$L_{i}$ arrives directly from a light source (direct illumination). i.e.:
$$
L_{i}(x, \vec{\omega}) = T_{r}(x, r(x, \vec{\omega})) L_{e}(r(x, \vec{\omega}), -\vec{\omega})
$$
#TODO: Equation on slide 40.
![[Single Scattering Volumetric Rendering.png]]
Do this for each point along the ray though the volume, sum them up, that builds the $\int_{0}^{z}$ integral.
#### Simple Solution
Assumptions:
- Homogeneous medium
- Point/spot light
- Simple phase function
- No occlusion
#TODO: Equation slide 45
#### General Solution
Gets really complicated, see Pegoraro et al. 2010.
#### Approximate Solution
Use [[Ray Marching]]. This is what we actually do.
### Multiple Scattering
#### Idea 1: Multiple Bounces
Use multiple bounces, as with Monte Carlo ray tracing.

Problem: This creates exponential growth of bounces within the volume, grows really quickly.

This is not feasible.
#### Idea 2: Volumetric Path Tracing
[[Volumetric Path Tracing]]
## Other Approaches
See Slides 16 Slide 112. Lots of new approaches.

[[Volumetric Photon Mapping]]