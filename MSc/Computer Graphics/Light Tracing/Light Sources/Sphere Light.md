Typically defined at point $p$ with radius $r$ and emitted [[Flux|Radiant Power]] $\Phi$ or [[Radiance]] $L_{e}$. Has finite area $4 \pi r^{2}$. Note: In Nori, it is defined with [[Radiance]].
## $L_{e}$
If defined with [[Radiance]], return $L_{e}$ directly.

#Unclear: $L_{e}$ for $\Phi$.
## Sampling
### Sampling Subtended Angle
Best approach: Uniformly sample [[Solid Angle]] [[Subtended Angle (Geometry)|subtended]] by the sphere.
![[Sphere Light Sampling Subtended.png|150]]
### Sampling Spherical Cap
Alternative 1: Sample area of the visible spherical cap. Problem: Emitted radiance is weighted by cosine term (See [[Reflection Equation#Surface Area Integration]] $G$ geometry term).
### Sampling Surface
Alternative 2: Rejection sampling on the whole surface.
### Sampling Caution: Measures
![[Sphere Sampling Caution.png]]
![[Sphere Sampling Caution Example.png]]
### Sampling Validation
![[Sphere Sampling Validation.png]]
