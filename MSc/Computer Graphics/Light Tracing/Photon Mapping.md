Motivation: [[Specular-Diffuse-Specular Paths]]
## Structure
Two passes:
1. Tracing of photons from light sources, caching them in a photon map. [[#Photon Tracing]]
2. Tracing from the eye and approximating indirect illumination using the photons [[#Rendering]]

Connect to eye subpaths using Kernel Density Estimation.
## Photon Tracing
Emit photons, scatter them and store them at randomly many of the bounces.
### Initial Definitions per Photon
- $x_{p}$: position
- $\vec{\omega}_{p}$: direction
- $\Phi_{p}$: photon power ([[Flux]], not [[Radiance]])
Via:
- Sample position from surface area of light from $p(x_{p})$
- Sample direction $p(\vec{\omega}_{p} | x_{p})$
- $\Phi_{p}$: #TODO 

#### Interesting Derivation
If PDFs are proportional to the emission, i.e.:
#TODO: Slide 61 formula
We get:
#TODO: Derivation $=\frac{\Phi}{M}$.

Where $\Phi$ is the total power of the light source and $M$ is the number of emitted photons.
### Generating the Map
```
repeat:
	(l, Prob_l) = chooseRandomLight()
	(x, omega, Phi) = emitPhotonFromLight(l)
	tracePhoton(x, omega, Phi / Prob_l)
until we have enough photons;
divide all photon powers by number of emitted photons;
```
### Tracing the Photon
- Hit surface
- Possibly store photon
- Sample BRDF/BSDF
- Calculate new power based on BSDF/BRDF
- Continue the bounces (Russian Roulette, re-weigh power)
Pseudocode on [[CG 07V2 Global Illumination III]] Slide 65.
#### Storing the photons
- Store only on diffuse (or moderately glossy) surfaces.
- Stored data can explode, use packing ([[CG 07V2 Global Illumination III]] Slide 67)
#### Path Termination
Use Russian Roulette with:
$$
q = \min\left( 1, \frac{\Phi'}{\Phi} \right)
$$
Update surviving power:
$$
\Phi' \leftarrow \frac{\Phi'}{q}
$$
Where $\Phi'$ is the power after the scattering event.
## Rendering
For each shading point:
- Find the $k$ closest photons
- Approximate radiance using density of photons
### Radiance Estimate
Estimate density based on Kernel Density Estimation.
#TODO: Slide 77

Using a non-constant kernel:
#TODO: Slide 82
### Selecting the Area
1. First define area, then find photons within
2. First find $k$ nearest photons, then define area
	1. Ignoring the $k$-th photon in the sum, but not in the area calculation (some heuristic there)
## Bias / Errors
- Darkening in corners
	- We assume a flat area around every point
- Blurring
	- Averaging over some radius
- Splotches
	- Random bunching of photons

Note: Photon count and found photons have to be relatively in balance. E.g. 100k photons and only 50 photons in the radiance estimate may be very splotchy.
## Improvements
### Caustic Improvements
#TODO: Slide 90
### Final Gather
Use MC ray tracing to push the density estimation (blotchy area) one bounce further from the camera.
## Testing
#TODO: Slide 97
## Pros and Cons
### Pros
- Handles difficult paths more robustly than unbiased algorithms
- Is a [[Consistent Estimator]]
- Reuse of computation (stored photons)
### Cons
- Bias
- Requires additional data structure to store photons
- No progressive rendering
- Large memory footprint
