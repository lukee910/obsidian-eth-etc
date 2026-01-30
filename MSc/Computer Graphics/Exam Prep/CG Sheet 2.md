## Part 1: Radiometric Quantities
[[Radiometric Quantities]]
### 1.1
Express [[Flux|Radiant Flux]] in terms of [[Radiance]]. Aka, do you remember the [[Rendering Equation]]?

Radiant Flux: Total amount of energy passing through a surface or region per unit time. Radiance: Flux per solid angle and area.

Relation:
$$
\Phi(A) = \int_{A} \int_{H^{2}} L(x, \vec{\omega}) \cos(\theta)\ d\vec{\omega}\ dA(x)
$$
### 1.2
[[Inverse Square Law]]
[[Irradiance]]
#### 1)
$$
\Phi(A) = \int_{A} E(x)\ dA(x)
$$
I think: $\Phi(A)$ is the flux _leaving the pointlight_, $A$ is the "pointlight surface".
#### 2)
![[CG Recap Geometry#Sphere]]
### 1.3 Point Light
[[Radiant Intensity]]
[[Solid Angle]]
### 1.4 Anisotropic point light
[[CG Recap Analysis#Integrating over the Hemisphere]]
## Part 2: Appearance Modeling
### 2.1 Critical Angle of total internal reflection
[[Snell's Law]]
### 2.2 Snell's Law as Vectors
[[Snell's Law]]
### 2.3 Phong
"normalized" Phong: ![[CG 04V1-2 Microfacets#Phong]]
![[CG 04V1-2 Microfacets#Blinn-Phong]]

Issue: $\vec{\omega}_{r} \cdot \vec{\omega}_{o}$ can become negative. Then we get a negative value for $f_r$. Note: Solution says non-real, but idk how they got that.

With Blinn-Phong, it's always an acute angle (since we reflect only in the hemisphere), so it's fine.
## Part 3: Monte Carlo Integration
[[_T Monte Carlo Integration]]
### 3.1 Jacobian Method
Jacobian Method: ![[CG 04V2 Monte Carlo#Transforming Between Distributions]]

![[CG Recap Analysis#Jacobian]]


