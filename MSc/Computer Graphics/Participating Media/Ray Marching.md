## For In-Scattering
[[Solving the Volume Rendering Equation#In-Scattered Radiance]]

#TODO: Setup picture.
#TODO: Sum formula slide 50
#TODO: $T_{r}$ formula Slide 52

#TODO: Splitting into multiple ray marches (slide 57)
## Choosing the Samples
Problems: Many samples, each is expensive. Idea: Importance sampling equivalence.
Process:
1. Ray-march and cache transmittance
2. Estimate in-scattering using MC integration
	1. Distribute samples $\propto$ (part of) the integrand
### Approach 1: Proportional to Transmittance
![[Ray Marching Propto Transmittance.png]]
### Approach 2: Equi-angular sampling
Proportional to variation of in-scattered radiance.
![[Ray Marching Propto In-Scattered Radiance.png]]
