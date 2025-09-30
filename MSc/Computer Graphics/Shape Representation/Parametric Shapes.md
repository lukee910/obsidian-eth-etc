## Parametric Curves in 2D

### Circle
$$
\begin{align}
	& p: \mathbb{R} \to \mathbb{R}^{2}\\
	& t \to p(t) = (x(t), y(t))
\end{align}
$$
Concretely:
$$
p(t) = r(\cos(t), \sin(t)),\ t \in [0, 2\pi )
$$
### Bezier Curves
For $n$ points:
$$
\begin{align}
s(t) &= \sum\limits_{i=0}^{n}\mathbf{p}_{i}B_{i}^{n}(t)\\
B_{i}^{n} (t) &= \binom{n}{i} t^{i} (1-t)^{n-i}
\end{align}
$$
## Parametric Curves in 3D
### Sphere
$$
\begin{align}
s &: \mathbb{R}^{2} \to \mathbb{R}^{3}\\
s(u,v) &= r\left( \cos(u) \cos(v), \sin(u) \cos(v), \sin(v) \right) \\
(u,v) &\in [0,2\pi) \times [-\pi/2,\pi/2]
\end{align}
$$
### Bezier Surface
On a grid of $m \times n$ points:
$$
s(u,v) = \sum\limits_{i=0}^{m} \sum\limits_{j=0}^{n} \mathbf{p}_{i,j} B_{i}^{m}(u) B_{j}^{n}(v)
$$
### NURBS surfaces
Non-uniform rational B-splines

Note: Use this instead of Bezier surfaces. Formulas see slides.
## Parametric Tangents and Normals
$$
\begin{align}
s_{u} &= \frac{\partial s(u,v)}{\partial u} \\
s_{v} &= \frac{\partial s(u,v)}{\partial v} \\
n &= \frac{s_{u} \times s_{v}}{\| s_{u} \times s_{v} \|}
\end{align}
$$
With $s_{u}, s_{v}$ being the tangents on the surface.




