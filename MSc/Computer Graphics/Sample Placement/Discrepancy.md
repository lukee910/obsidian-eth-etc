## Idea
Formal definition of "clumping" (see [[Sample Placement - Overview]]).
## Defintion
Clumping $D(x_{1}, \ldots, x_{n})$:

$$
D(x_{1}, \ldots, x_{n}) = \sup_{b\in\mathcal{D}} \left| \frac{s_{b}(x_{1}, \ldots, x_{n})}{n} - V(b) \right| 
$$
Where $s_{b}$ are the samples in region $b$, $V(b)$ is the volume of region $b$.
## Star Discrepancy
$D^{*}(x_{1}, \ldots, x_{n})$ only considers rectangles with one vertex at the origin.
## Koksma-Hlawka Inequality
Discrepancy gives an upper bound on the estimation error:
$$
\left| \frac{1}{n} \sum\limits_{i=1}^{n} f(x_{i}) - \int f(u)\ du \right| \leq V(f) D^{*}(x_{1}, \ldots, x_{n})
$$
Where:
- $V(f)$: Total variation of the integrand
- $D^{*}(x_{1}, \ldots, x_{n})$: Discrepancy of samples
