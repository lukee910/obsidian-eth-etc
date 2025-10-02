Given: First order ODE $y' = f(t,y)$, Initial conditions $y(t_{0}) = y_{0}$.
Result: Solve for $y(t)$.

In general: No analytical solution, have to approximate.
## Notation and General
* $y(t)$ true solution
* $t_{i}$ approximate solution at time $t_{i} = t_{0} + i \cdot h$
* $h$ time step size (constant)
### Approximation Problem Definition
Given $y_n$, compute $y_{n+1}$.
### Taylor Series Expansion
$y(t+h) = y(t) + hy'(t) + \frac{h^{2}}{2!}y''(t) + \ldots$ 
## Numerical Integration
Field of approximating ODEs numerically with this idea:
$$
y(t+h) = y(t) + \int_{t}^{t+h} y'(t) dt
$$
$\Rightarrow$ Approximations $y_i$ to true solution at discrete time instants $t_i$. Compute $t_{i+1}$ based on $t_{i}, t_{i-1}, \ldots$
### Evaluating and Comparing Schemes
[[Evaluating and Comparing Integration Schemes]]
## Approximations on Taylor Expansions
### First Order Taylor
Use [[Solving ODEs#Taylor Series Expansion|Taylor Expansion]] on the first order approximation:
$$
y(t+h) = y(t) + hy'(t) + \mathcal{O}(h^2)
$$
Assume the first order derivation is known.
### Second Order Taylor
Use [[Solving ODEs#Taylor Series Expansion|Taylor Expansion]] on the second order approximation:
$$
y(t+h) = y(t) + hy'(t) + \frac{h^{2}}{2!}y''(t) + O(h^3)
$$
Problem: High order derivations may not be known.
## Integration Perspective Overview
![[Integration Perspective.png]]
[[Solving ODEs#Explicit Euler]]
#TODO: Implicit Euler Link
[[Solving ODEs#Explicit Midpoint]]
## Methods
#TODO: List pros and cons per method
### Explicit Euler
[[Solving ODEs#First Order Taylor|First Order Taylor]]

Calculation:
$$
y_{n+1} = y_{n} + hf(t_{n}, y_{n})
$$
### Implicit Euler
[[Solving ODEs#First Order Taylor|First Order Taylor]]

Calculation:
$$
y_{n+1} = y_{n} + h f(t_{n+1}, y_{n+1})
$$
### Finite Differences
[[Solving ODEs#Second Order Taylor|Second Order Taylor]]

Approximate $y''$ with finite differences
$$
y''(t) = \frac{y'(t+h) - y'(t)}{h} + O(h)
$$
Note: $y'(t+h)$ can be estimated by [[Solving ODEs#Explicit Euler|Explicit Euler]] step.
Note: Still $\mathcal{O}(h^3)$, since $y''$ is multiplied with $h^2$.
### Explicit Midpoint
[[Solving ODEs#Second Order Taylor|Second Order Taylor]]

Combine backward and forward expansions:
$$
\begin{align}
y(t) &= y\left(t + \frac{h}{2}\right) - \frac{h}{2} y'\left(t + \frac{h}{2} \right) + \frac{h^{2}}{4}y''\left( t + \frac{h}{2} \right) - \mathcal{O}(h^{3}) \quad \text{Backward} \\
y(t+h) &= y\left(t + \frac{h}{2}\right) + \frac{h}{2} y'\left(t + \frac{h}{2} \right) + \frac{h^{2}}{4}y''\left( t + \frac{h}{2} \right) + \mathcal{O}(h^{3}) \quad \text{Forward}
\end{align}
$$
$\Rightarrow$
$$
y(t+h) = y(t) + hy'\left(t + \frac{h}{2}\right)+ O(h^{3})
$$
Note: Approximate slope at midpoint with Explicit Euler.

Note: Similar effort to Explicit Euler at step size $\frac{h}{2}$, however error is much better.
