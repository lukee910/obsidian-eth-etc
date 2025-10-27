## Setup
[[3D Case for Continuum Mechanics#Deformation Gradient|Deformation Gradient]] $F$ maps undeformed vectors to deformed vectors, $d = F\bar{d}$. In general, both the direction and length of $\bar{d}$ will change. 

Note: $F$ is linear in displacements.

How can we quantify the deformation in a given direction? (To tell stuff apart)
Measuring the length squared in any direction $d$:
$$
\begin{align}
|d|^{2} - |\bar{d}|^{2} &= d^{T}d - \bar{d}^{T}\bar{d} \\
&= (F\bar{d})^{T}(F \bar{d}) - \bar{d}^{T}\bar{d} \\
&= \bar{d}^{T}(F^{T}F - I)\bar{d}
\end{align}
$$
From this we get the [[#Green Strain]]:
## Green Strain
$$
E = \frac{1}{2}(F^{T}F - I)
$$
Idea: Nonlinear measure of deformation, quadratic in deformation gradient.

Quadratic in displacements:
$$
E = \frac{1}{2}(F^{T}F - I) = \frac{1}{2} (\nabla u + \nabla u^{T} + \nabla u^{T} \nabla u)
$$

Discarding quadratic terms leads to the linear [[#Cauchy Strain]]:
## Cauchy Strain
$$
\varepsilon = \frac{1}{2} (\nabla u + \nabla u^{T}) = \frac{1}{2} (F + F^{T}) - I
$$
Idea: Simpler than [[#Green Strain]].

Written out:
$$
\varepsilon = \frac{1}{2} \begin{pmatrix}
2 \partial_{x} u & \partial_{y} u + \partial_{x} v & \partial_{z} u + \partial_{x} w \\ \partial_{x}v + \partial_{y} u & 2\partial_{y}v & \partial_{z}v + \partial_{y}w \\ \partial_{x}w + \partial_{z}u & \partial_{y}w + \partial_{z}v & 2\partial_{z} w
\end{pmatrix}
$$
Linear function. Loses accuracy.
## Green Strain vs Cauchy Strain
### Rotations
Nonlinear Green strain is invariant under rotations: Apply incremental rotation R to given deformation $F$ to obtain $F' = RF$

Green:
$$
E' = \frac{1}{2}(F'^{T} F' - I) = \frac{1}{2}(F^{T}R^{T}RF - I) = \frac{1}{2}(F^{T}F - I) = E
$$
Cauchy:
$$
\varepsilon' = \frac{1}{2}(F' + F'^{T}) - I = \frac{1}{2}(RF + F^{T} R^{T}) - I \neq \varepsilon
$$
We have:
* Elastic energy changes for Cauchy, but not for Green (we don't want it to change)
* Cauchy has artifacts for Rotations
### Using Green vs Cauchy
If you want precision, use Green. However, it's much more complex to compute.