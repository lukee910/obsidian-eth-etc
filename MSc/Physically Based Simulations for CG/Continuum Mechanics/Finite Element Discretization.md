Not [[Proper FEM Discretization]]

## Overview
- Divide input model into elements (e.g. triangles, tetrahedra)
- For each element, evaluate its energy, the energy gradient and the energy Hessian
- All quantities depend (only) on the [[3D Case for Continuum Mechanics#Deformation Gradient|Deformation Gradient]] $F$.
## Finite Element
A finite element consists of:
- A closed subset $\Omega_{e} \subset \mathbb{R}^d$ with $n$ vectors of nodal positions $\bar{x}_{i} \in \mathbb{R}^{d}$ describing the reference geometry.
- $n$ vectors of degrees of freedom (e.g., deformed positions $x_{i}$).
- $n$ nodal basis functions $N_{i} : \Omega_{e} \to \mathbb{R}$.
### Nodal Basis Functions
We can always compute them. From the triangle example:

![[Finite Element Triangle.png]]
Basis functions are linear: $N_{i}(\bar{x},\bar{y}) = a_{i}\bar{x} + b_{i}\bar{y} + c_{i}$.

From $N_{i}(\bar{x}_{j}) = \delta_{ij}$ (Chirac delta, basis functions must interpolate and be 1 only at their node) we obtain:
$$
\begin{bmatrix}
x_{1} & y_{1} & 1 \\ x_{2} & y_{2} & 1 \\ x_{3} & y_{3} & 1
\end{bmatrix} \cdot \begin{bmatrix}
a_{i} \\ b_{i} \\ c_{i}
\end{bmatrix} = \begin{bmatrix}
\delta_{1i} \\ \delta_{2i} \\ \delta_{3i}
\end{bmatrix}
$$
Solve by inverting:
$$
\begin{bmatrix}
a_{i} \\ b_{i} \\ c_{i}
\end{bmatrix} = 
\begin{bmatrix}
x_{1} & y_{1} & 1 \\ x_{2} & y_{2} & 1 \\ x_{3} & y_{3} & 1
\end{bmatrix}^{-1} \cdot \begin{bmatrix}
\delta_{1i} \\ \delta_{2i} \\ \delta_{3i}
\end{bmatrix}
$$
So we can always compute the basis functions.

Works for tetrahedra as well, just add a dimension.

Use the basis functions to define continuous geometry of element as: #TODO
### Deformation Gradient
$$
F = I + \frac{\partial u(\bar{x})}{\partial \bar{x}} = \frac{\partial x(\bar{x})}{\partial \bar{x}} = \sum\limits_{i} x_{i} \left( \frac{\partial N_{i}}{\partial \bar{x}} \right)^{T}
$$
Note: $F \in \mathbb{R}^{3x3}$ and $F$ is linear in $x_{i}$. $N_{i}$ are linear on element $\to$ $F$ is constant across element.
