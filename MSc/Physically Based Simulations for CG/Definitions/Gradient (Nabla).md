---
aliases:
  - Gradient
  - $\nabla$
---
Gradient operator $\nabla$

Note the syntax: $\nabla \cdot \mathbf{u} \neq \nabla \mathbf{u}$ (see [[Divergence]])
## Definition
$$
\nabla u = \begin{bmatrix}
\frac{\partial u}{\partial x_{1}} \\ \vdots \\ \frac{\partial u}{\partial x_{n}}
\end{bmatrix}
$$
Note:
- Applies on vectors and scalar functions
- For $u : \mathbb{R}^{n}$, we have $\nabla u \in \mathbb{R}^{n \times n}$. If applied to function $f : \mathbb{R}^{n} \to \mathbb{R}$, we have $\nabla f \in \mathbb{R}^{n} \to \mathbb{R}^{n}$.
## Notes
### Thinking About $\nabla$
Consider: How fast does $f(x, y, z) : \mathbb{R}^{3} \to \mathbb{R}$ change along a given direction $\Delta \mathbf{x} = (\Delta x, \Delta y, \Delta z)$?
$$
\begin{align}
\Delta f &= \frac{\partial f}{\partial x}\Delta x + \frac{\partial f}{\partial y}\Delta y + \frac{\partial f}{\partial z}\Delta z + \mathcal{O}(\Delta \mathbf{x}^{2}) \\
&= \nabla f^{T} \Delta \mathbf{x} + \mathcal{O}(\Delta \mathbf{x}^{2})
\end{align}
$$
