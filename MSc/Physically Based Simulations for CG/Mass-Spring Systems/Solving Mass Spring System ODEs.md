Implicitly.

## Setup
Per node:
$$
m\mathbf{a_{i}} = \mathbf{f_{i}} \quad \text{ where } \mathbf{f_{i}} = \sum_{j} \mathbf{f}_{ij}^{spring} + m \mathbf{g}
$$
Convert to system of first-order ODEs:
$$
\begin{align}
	\mathbf{\dot{x}} &= \mathbf{v} \\
	\mathbf{\dot{v}} &= \mathbf{M^{-1}}\mathbf{f(x)}
\end{align}
$$
Discretize with [[Solving ODEs#Implicit Euler]]:
$$
\begin{align}
	\mathbf{x}_{n+1} &= \mathbf{x}_{n} + h\mathbf{v}_{n+1} \\
	\mathbf{v}_{n+1} &= \mathbf{v}_{n} + h\mathbf{a}_{n+1} = \mathbf{v}_{n} + h \mathbf{M^{-1}}\mathbf{f}(\mathbf{x}_{n+1})
\end{align}
$$
Note: vs explicit, here we don't know all values ($v,x_{n+1}$).

Rewrite with positions $x_{n+1}$ only as unknowns:
$$
\begin{align}
x_{n+1} = x_{n} + hv_{n+1} &= x_{n} + hv_{n} + h^{2}M^{-1} f(x_{n+1}) \\
\text{with}\quad hv_{n+1} &= h(v_{n} + h M^{-1}f(x_{n+1}))
\end{align}
$$
Take $x_{n+1}$ to one side:
$$
\begin{align}
g(x_{n+1}) &= M(x_{n+1} - x_{n} - hv_{n}) - h^{2} f(x_{n+1}) \\
&= M(x_{n+1} - x_{n}) - h^{2} f(x_{n+1}) - hMv_{n} \\
&= 0 \\
\end{align}
$$
Non-linear equations $\Rightarrow$ Solve with Newton's method.
### Applying Newton's Method
![[Newton's method on g(x_n+1)=0.png]]
#TODO : How do Euler steps and newton's method interact?

Problems:
* System matrix may be singular or non-definite
* Taking full steps may lead to divergence
	* Systems are not as linear as we assume in reality
* No reliable progress indicator for generic root finding problems
### Analyzing the Jacobian
Recall: $g(x_{n+1}) = M(x_{n+1} - x_{n}) - h^{2} f(x_{n+1}) - hMv_{n}$.
$$
\begin{align}
\frac{\partial g}{\partial x} |_{x=x_{n+1}} &= M - h^{2} \frac{\partial f}{\partial x}- h \frac{\partial f}{\partial v}\frac{\partial v}{\partial x} \\
 &= M - h^{2} \frac{\partial f}{\partial x} - h \frac{\partial f}{\partial v}
\end{align}
$$
($\frac{\partial f}{\partial v}\frac{\partial v}{\partial x}$ via chain rule)

Note: We need Jacobian of force $J = \frac{\partial f}{\partial x}$.
Recall: Forces are the negative gradient of energy: $f = -\frac{\partial E}{\partial x}$.
$\Rightarrow$ Jacobian $J = \frac{\partial f}{\partial x} = -\frac{\partial^{2} E}{\partial x^{2}} = -H$, the energy Hessian.
We know that second derivatives commute, so we can sum up contributions from individual springs:
$$
E = \sum\limits_{k} E_{k} \quad \to \quad H = \frac{\partial^{2} E}{\partial x^{2}} = \sum\limits_{k} \frac{\partial^{2} E_{k}}{\partial x^{2}}
$$
### Hessian
Hessian for a given spring:
$$
H_{ij}^{k} = \frac{\partial^{2} E_{k}}{\partial x_{i} \partial x_{j}}
$$
Note: Hessian in 3D is a $6 \times 6$ matrix, each point has $3$ degrees of freedom:
$$
H^{k} = \begin{bmatrix}
\frac{\partial^{2} E}{\partial x_{1} \partial x_{1}} & \frac{\partial^{2} E}{\partial x_{1} \partial x_{2}} \\ \frac{\partial^{2} E}{\partial x_{2} \partial x_{1}} & \frac{\partial^{2} E}{\partial x_{2} \partial x_{2}}
\end{bmatrix}
$$
Where each of these entries is $\in \mathbb{R}^{3 \times 3}$.

Facts about $H$:
* $H$ is block-structured: See above.
* $H$ is symmetric: $H_{ij} = H_{ji}^{T}$
* $H$ is sparse: $H_{ij}$ is only nonzero if there is a spring between the nodes $i$ and $j$.
