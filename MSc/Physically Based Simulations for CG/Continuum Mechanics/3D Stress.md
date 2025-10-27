## Setup
![[3D CM FEM Stress Setup.png|150]]
Intersect cut plane with normal $n$ through point $x$. Observe traction force $f(x,n)$ on area $dA$. Traction force density $t(x,n) = \frac{df}{dA}$ as $dA \to 0$.

How does $t$ change with $n$?
## Cauchy's Stress Theorem
$t$ depends linearly on $n$:
$$
t(x,n) = \sigma(x) \cdot n
$$
Cauchy stress tensor written out:
$$
\sigma(x) \cdot n = \begin{pmatrix}
\sigma_{x} & \tau_{xy} & \tau_{xz} \\ \tau_{xy} & \sigma_{y} & \tau_{yz} \\ \tau_{xz} & \tau_{yz} & \sigma_{z}
\end{pmatrix}
$$
* $\sigma_{i}$: Normal stress components (def. see [[1D Case for Continuum Mechanics#Setup]])
* $\tau_{ij}$: Shear stress components
Entries of $\sigma$ are force components on unit cube (for constant stress):
![[Cauchy Stress Cube.png]]
## Stress Equilibrium
Stress varies spatially. Consider traction forces acting on the unit cube:
![[3D Stress Force Balance Unit Cube.png]]
We will focus on the x axis.

### Internal Force Density of Stress
x-component of the internal force density:
$$
\frac{f_{x}}{dx \cdot dy \cdot dz} = \frac{\sigma_{x}(x+dx) - \sigma_{x}(x)}{dx} + \frac{\tau_{xy}(y + dy) - \tau_{xy}(y)}{dy} + \frac{\tau_{xz}(z + dz) - \tau_{xz}(z)}{dz}
$$
For $dx,dy,dz \to 0$, these terms approach a derivative:
$$
\ldots = \frac{\partial}{\partial x}\sigma_{x} + \frac{\partial}{\partial y} \tau_{xy} + \frac{\partial}{\partial z} \tau_{xz}
$$

Doing this for all components:
$$
\frac{f_{int}}{dV} = \begin{pmatrix}
f_{x} \\ f_{y} \\ f_{z}
\end{pmatrix} = \begin{pmatrix}
\frac{\partial}{\partial x}\sigma_{x} + \frac{\partial}{\partial y} \tau_{xy} + \frac{\partial}{\partial z} \tau_{xz} \\ \frac{\partial}{\partial x}\tau_{xy} + \frac{\partial}{\partial y} \sigma_{y} + \frac{\partial}{\partial z} \tau_{yz} \\ \frac{\partial}{\partial x}\tau_{xz} + \frac{\partial}{\partial y} \tau_{yz} + \frac{\partial}{\partial z} \sigma_{z}
\end{pmatrix} = \nabla \cdot \sigma
$$
### Governing PDE for Stress
$$
\nabla \cdot \sigma + f^{b} = 0
$$
(Strong form)

Note: Very complicated. We'll rarely use this, instead use [[Discrete Energy Approach]] (see [[Linear Elasticity Model]]).
#### Derivation of internal stress x-component
Note: Each of these three terms describes the stress at the two faces of each axis of the unit cube.

For the x-axis-faces, we look at the normal stress $\sigma_{x}$. The total force is $\sigma_{x}(x) \cdot (-dy\ dz)$ from the "back" face, plus $\sigma_{x}(x + dx) \cdot (dy\ dz)$ from the "front" face. Over all, that's $(\sigma_{x}(x + dx) - \sigma_{x}(x)) \cdot dy\ dz$. The $dy\ dz$ gets cancelled on $\frac{f_{x}}{dx \cdot dy \cdot dz}$.

The other faces contribute only sheer stress. The same type of operation and cancellation happens.
