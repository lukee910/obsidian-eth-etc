Sphere: $4\pi$ steradians.
$$
\Omega = \frac{A}{r^{2}}
$$
![[Solid Angle.png]]
## Subtended Solid Angle
Length/area of an objects projection onto a unit circle/sphere.
![[Subtended Solid Angle.png]]
## Differential Solid Angle
With:
* $\theta$: Angle on z axis
* $\phi$: Angle on x-y-plane
* $r$: Radius
![[Differential Solid Angle.png]]
Formulas:
$$
\begin{align}
dA &= (r\ d\theta)(r \sin(\theta)\ d\phi) \\
d\overrightarrow{\omega} &= \frac{dA}{r^{2}} = \sin(\theta)\ d\theta\ d\phi
\\
\Omega &= \int_{S^{2}} 1\ d\overrightarrow{\omega} = \int^{2\pi}_{0}\int^{\pi}_{0} \sin(\theta)\ d\theta\ d\phi = 4\pi
\end{align}
$$
Notes:
* $dA$
	* Differential Area
	* Small square on sphere
	* $r\sin(\theta)\ d\phi$ is the length across, needs to be scaled since it's "squished" the higher you go
	* $r\ d\theta$ is the length along. No need to squish, stays the same.
* $d\overrightarrow{\omega}$
	* Differential solid angle
* $\Omega$
	* Full sphere solid angle
	* $\Omega = \frac{A}{r^{2}}= \int_{S^{2}} \frac{dA}{r^{2}}= \int_{S^{2}} 1\ d\overrightarrow{\omega} = \ldots$
