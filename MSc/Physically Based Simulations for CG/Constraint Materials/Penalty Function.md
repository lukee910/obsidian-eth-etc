## Penalty Function
Define a penalty function (potential energy) for a [[Constraint]]. Easy choice is polynomial, and within polynomial quadratic usually makes sense:
$$
E_{C}(x_{1}, \ldots, x_{n}) = \frac{1}{2}kC(x_{1}, \ldots, x_{n})^{2}k
$$
Where $k$ is a stiffness coefficient.

Observe that $E_{C} = 0$ if constraint is satisfied, $E_{C} > 0$ if not satisfied.