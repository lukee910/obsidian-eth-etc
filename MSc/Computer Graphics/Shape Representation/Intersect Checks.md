## Ray-Sphere Intersection
[[Parametric Shapes#Sphere]]
### Geometric Approach
Intersection at:
$$
t = (\mathbf{c} - \mathbf{o}) \cdot \mathbf{d} \pm \sqrt{r^{2} - D^{2}}
$$
Where $D$ is the distance of the closest point on the ray to the center.
$$
D^{2} = \| \mathbf{c} - \mathbf{o} \|^{2} - ((\mathbf{c} - \mathbf{o}) \cdot \mathbf{d})^{2}
$$
Reject intersection if:
* $\mathbf{o}$ not in sphere and $(\mathbf{c} - \mathbf{o}) \cdot \mathbf{d} < 0$: Ray pointing away from sphere
* $r^{2} - D^{2} < 0$: Nearest distance of ray outside of sphere
![[Ray-Sphere Intersection Sketch.png]]
Process:
1. Compute origin-center distance: $\|\mathbf{c} - \mathbf{o}\|^{2}$
2. Compute ray distance ($t$) that is closest to center: $(\mathbf{c} - \mathbf{o}) \cdot \mathbf{d}$
	1. (Projects origin-center vector onto ray)
3. Compute shortest distance squared from ray to center: $D^{2}$
4. Compute half-chord distance squared: $\sqrt{r^{2} - D^{2}}$
5. Compute $t$: See above.
### Algebraic Approach
(Not used in this subject)
Insert ray equation $r(t) = \mathbf{o} + t\mathbf{d}$ in sphere equation, solve for $t$.
$$
\| \mathbf{o} + t\mathbf{d} - c \|^{2} - r^{2} = 0
$$

Derive via: $$
\begin{align}
(\mathbf{o_{x}} + t\mathbf{d}_{x} - \mathbf{c}_{x})^{2} &+ \\ 
(\mathbf{o_{y}} + t\mathbf{d}_{y} - \mathbf{c}_{y})^{2} &+ \\
(\mathbf{o_{z}} + t\mathbf{d}_{z} - \mathbf{c}_{z})^{2} &- r^{2} = 0
\end{align}
$$
Reduces to $At^{2} + Bt + C = 0$, solve with quadratic equation.

## Ray-Plane Intersection
#TODO: This
## Ray-Triangle Intersection
#TODO: This
2 approaches.
