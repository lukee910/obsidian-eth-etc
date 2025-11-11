See [[Curvature of Curves]].
## Idea
How fast do the tangents (multiple) change in the normal direction when varying the parameters.
#TODO: Chart on slides 08 slide 4, setup
#TODO: Thing he mentioned about getting the tangents from the maps, and the maps themselves
## Definition
Curvature in different directions via:
Second Fundamental Form:
$$
\mathrm{I\!I} = \begin{bmatrix}
x_{uu}^{T} n & x_{uv}^{T} n \\ x_{vu}^{T}n & x_{vv}^{T}n
\end{bmatrix}
$$
## Types
### Normal Curvature 
$\kappa_{n}(t)$
1. Choose point, get normal
2. Get any tangent direction
3. Calculate curve on the curve spanned by norm and tangent
### Principal Curvatures
- $\kappa_{1} = \min_{t} \kappa_{n}(t)$
- $\kappa_{2} = \max_{t} \kappa_{n}(t)$
### Mean Curvature
$$
H = \frac{1}{2}(\kappa_{1} + \kappa_{2})
$$
### Gaussian Curvature
$$
K = \kappa_{1} \cdot \kappa_{2}
$$
## Examples
Cylinder: $H \neq 0,\ K = 0$, constant
Sphere: $H \neq 0,\ K \neq 0$, constant
Hyperbolic Tower thing: $H = ?,\ K < 0$. $K$: Min and max always have different signs.
![[Surface Curvature Examples.png]]
