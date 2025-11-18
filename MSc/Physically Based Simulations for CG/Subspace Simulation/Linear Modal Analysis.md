Analyze low-frequency deformations.

Idea: We're more interested in slow, significant movements, rather than jitters or ripples.

Q: What deformations are easy to induce? A: Those that require little work (i.e. effort).
## Example: Quadratic system with elastic energy
### Setup
$$
E(u) = \frac{1}{2} u^{T} H u + b^{T}u + c
$$
Where $u = x - \bar{x}$ are displacements, $x$ deformed positions and $\bar{x}$ reference points. $H$ hessian of energy.

We want $E(0) = 0$ and $\frac{\partial E}{\partial x} = 0$ at $0$, so $b=0,\ c=0$.
### Deformations
What displacements of given magnitude induce the least energy?
- Rigid translation, rigid rotation (but those are boring)
- Something else?

Optimization problem:
$$
\min_{v} \frac{1}{2} v^{T} H v
$$
s.t. $\frac{1}{2}(v^{T}v - 1) = 0$
Corresponding Lagrangian:
$$
L(v, \lambda) = \frac{1}{2}v^{T}Hv - \frac{\lambda}{2}(v^{T}v - 1)
$$
First-order optimality conditions:
$$
\frac{\partial L}{\partial v} = Hv - \lambda v = 0 \Rightarrow Hv = \lambda v
$$
We get the Eigenvalue problem. Notably, the eigenvector with the smallest eigenvalue is the global minimum. These eigenvalues are also called Eigenmodes.

Note:
- $\min_{v} \frac{1}{2}v^{T}Hv$ is convex
- Constraint $\frac{1}{2}(v^{T}v - 1) = 0$ unit vectors is not convex, since any vector between two unit vectors is not unit length

Note: We get 6 rigid modes in 3D, corresponding to translation and rotation. Since they are all 0, the exact modes are arbitrary and can combine rotation and translation.
