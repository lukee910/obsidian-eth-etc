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
## Evaluating Integration Schemes
* Convergence
	* Do approximations converge to true solution $y_{i} \to y(t_{i})$ for $h \to 0$?
* Accuracy
	* How fast does the error $|y_{i} - y(t_{i})|$ decrease as $h \to 0$?
* Stability
	* Is the solution always bounded, $|y_{i}| < \infty$?
* Efficiency
	* Is a given method a good choice for a given problem?
	* Definition depends on situation.
### Error
Global Error (usually unavailable):
$$
|y_{i} - y(t_{i})|
$$

Local Error (Single Step):
$$
\left| \left( y_{n} + \int^{t_{n}}_{t_{n+1}} f(t, y(t)) dt \right) - y_{n+1} \right|
$$
As a function of the step size, how large is the error for my current step?
### $p$-Accuracy
A method with local error $\mathcal{O(h^{p+1})}$ is $p$-accurate.
## Explicit Euler
Use [[Solving ODEs#Taylor Series Expansion|Taylor Expansion]] on the first order approximation:
$$
y(t+h) = y(t) + hy'(t) + \mathcal{O}(h^2)
$$
Calculation:
$$
y_{n+1} = y_{n} + hf(t_{n}, y_{n})
$$
## TEMP
Use [[Solving ODEs#Taylor Series Expansion|Taylor Expansion]] on the second order approximation: $y(t+h) = y(t) + hy'(t) + \frac{h^{2}}{2!}y''(t) + O(h^3)$.

Problem: High