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
### 1.4 Anisotropic Point Light
[[CG Recap Analysis#Integrating over the Hemisphere]]
## Part 2: Appearance Modeling
### 2.1 Critical Angle of Total Internal Reflection
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
[[Jacobian]]
Jacobian Method: ![[CG 04V2 Monte Carlo#Jacobian Method]]
#### 1)
$z = x^{\frac{2}{3}}$:
1. $T_{Z}^{-1}(z)$: $z = x^{\frac{2}{3}} \Leftrightarrow z^{\frac{3}{2}} = x$
2. $\frac{dx}{dz}$: $\frac{dx}{dz} = \frac{d}{dz} z^{\frac{3}{2}} = \frac{3}{2}z^\frac{1}{2}$
3. $p_{Z}(z)$: $p_{Z}(z) = p_{X}(x) \left| \frac{dx}{dz} \right|$
   $p_{X}(x)$ range: $z \in [0, 1[ \Rightarrow z^{\frac{3}{2}} \in [0, 1[ \Rightarrow x \in [0, 1[$. We get:
   $$p_{Z}(z) = \begin{cases}
1 \cdot \left| \frac{3}{2} \sqrt{z} \right| = \frac{3}{2} \sqrt{z} & z \in [0, 1[  \\
0 & else
\end{cases}$$


### 3.2 Malley's Method
Same as this: [[CG 04V2 Monte Carlo#Cosine-Weighted Hemispherical Sampling]]
Prove that this is correct.
### 3.3 Uniformly Sampling a Ring
Same steps as [[#3.2 Malley's Method]].
#TODO 
