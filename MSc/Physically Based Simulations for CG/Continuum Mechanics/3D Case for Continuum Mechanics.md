## Setup
* Undeformed State $\bar{\Omega} \subset \mathbb{R}^{3}$, described by positions $\bar{x}$
* Deformed State $\Omega \subset \mathbb{R}^{3}$, described by positions $x$
### Displacement Field
Displacement field $u$ maps from $\bar{\Omega}$ to $\Omega$
![[3D CM FEM setup.png|600]]
Note: $u$ doesn't connect to energy as easily. Imagine moving an object to the right, has a displacement but no additional stored energy.
### Deformations
Choose (undeformed) material points $\bar{x}_{1}, \bar{x}_{2}$ and $\bar{d} = \bar{x}_{2} - \bar{x}_{1}$ s.t. $|\bar{d}|$ is infinitesimal.
![[Displacement Vector Deformed.png|300]]

Consider deformed vector $d$:
$$
\begin{align}
d = x_{2} - x_{1} &= \bar{x}_{2} + u(\bar{x}_{2}) - \bar{x}_{1} - u(\bar{x}_{1}) \\
&= \bar{d} + u(\bar{x}_{1} + \bar{d}) - u(\bar{x}_{1}) \\
(\text{1st order Taylor}) &\approx \bar{d} + u(\bar{x}_{1}) + \nabla u \bar{d} - u(\bar{x}_{1}) \\
&= (I + \nabla u) \bar{d}
\end{align}
$$
With:
$$
\nabla u = \begin{pmatrix}
\partial_{x} u & \partial_{y} u & \partial_{z} u \\ \partial_{x} v & \partial_{y} v & \partial_{z} v \\ \partial_{x} w & \partial_{y} w & \partial_{z} w \\
\end{pmatrix}
$$
(because of the definition of $u(x)$ in [[#Displacement Field]])
#### Deformation Gradient
$$
F = (I + \nabla u)
$$
Maps undeformed vectors to deformed vectors, $d = F\bar{d}$.
## 3D Nonlinear Strain
[[3D Nonlinear Strain]]
## 3D Stress
[[3D Stress]]
## Elasticity Models
Try to describe the relation between strain and stress, as well as energy.
### Linear Elasticity Material Model
Describe the relation between stress and strain in a simplified model:
[[Linear Elasticity Model]]
### Nonlinear Elasticity
[[Nonlinear Elasticity]]
## Finite Elements
Then, we have to discretize it:
[[Finite Element Discretization]]
