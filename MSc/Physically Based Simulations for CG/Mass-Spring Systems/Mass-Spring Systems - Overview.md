1. Spatial Discretization
2. Forces
3. Dynamics
4. Temporal discretization
## Spatial Discretization
[[Spatial Discretization]]
Sample object with mass points
## Forces
Define internal and external forces. Use [[Hookean Springs]].

Real-world mechanical systems dissipate energy over time (internal friction $\to$ thermal energy $\to$ outside of the system). Therefore, apply damping to simulate controllable diffusion. [[Damped Systems]].
### Linear Damping Force
$f^{visc} = -\gamma v$
Simple, but dampens all motion (also translation and rotation)
