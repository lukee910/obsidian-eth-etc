Sphere: $4\pi$ steradians.
$$
\Omega = \frac{A}{r^{2}}
$$
![[Solid Angle.png|600]]
## Subtended Solid Angle
Length/area of an objects projection onto a unit circle/sphere. See: [[Subtended Angle (Geometry)]]
![[Subtended Solid Angle.png|600]]
## Differential Solid Angle
With:
* $\theta$: Angle on z axis
* $\phi$: Angle on x-y-plane
* $r$: Radius
![[Differential Solid Angle.png|300]]
### Formulas
$$
\begin{align}
dA &= (r\ d\theta)(r \sin(\theta)\ d\phi) \quad \text{(Two sides that can be varied)} \\
d\overrightarrow{\omega} &= \frac{dA}{r^{2}} = \sin(\theta)\ d\theta\ d\phi
\\
\Omega &= \int_{S^{2}} 1\ d\overrightarrow{\omega} = \int^{2\pi}_{0}\int^{\pi}_{0} \sin(\theta)\ d\theta\ d\phi = 4\pi
\end{align}
$$
### Notes
- Idea: How much "area" is covered by the traversing over the entire specified angle?
	- Same idea as with any integration, the square represents the tangent
	- $r \sin \theta$ is the radius of the horizontal circle at $\vec{\omega}$ around the sphere, $r$ is the vertical circle radius.
* $dA$
	* Differential Area
	* (Infinitesimally) small square on sphere
	* $r\sin(\theta)\ d\phi$ is the length across, needs to be scaled since it's "squished" the higher you go
	* $r\ d\theta$ is the length along. No need to squish, stays the same.
* $d\overrightarrow{\omega}$
	* Differential solid angle
* $\Omega$
	* Full sphere solid angle
	* $\Omega = \frac{A}{r^{2}}= \int_{S^{2}} \frac{dA}{r^{2}}= \int_{S^{2}} 1\ d\overrightarrow{\omega} = \ldots$
