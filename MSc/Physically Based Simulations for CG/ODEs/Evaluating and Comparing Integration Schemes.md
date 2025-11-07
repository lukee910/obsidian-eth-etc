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
## Comparing Integration Schemes
Comparing is challenging, depends on the case/model.
### Dahlquist's Test Equation

| Test Equation        | Analytical Solution        |
| -------------------- | -------------------------- |
| $y'(t)=\lambda y(t)$ | $y(t)= e^{\lambda t}y_{0}$ |

For $\lambda \in \mathbb{R}$:
* $\lambda < 0$: Exponential Decay (e.g. [[Damped Systems]])
* $\lambda > 0$: Exponential Growth

For $\lambda \in \mathbb{C}$: $\lambda = a+ib \Rightarrow y(t) = y_{0} \cdot e^{at} \cdot e^{ibt}$
Where: $e^{at}$ models damping, $e^{ibt}$ models oscillation (cos on real axis, sin on imaginary axis) ($e^{i tb} = \cos(tb) + i \sin(tb)$, [[Euler's Formula (Complex Exponential)|Euler's Formula]])
Then we get:
* $a < 0$: Damped oscillator
* $a = 0$: Undamped oscillator
* $a > 0$: Unstable

For us interesting, **case with damping**.
### Schemes on the Test Equation
#### Explicit Euler
[[Solving ODEs#Explicit Euler]]
Explicit Euler Update: $y_{n+1} = y_{n} + h \lambda y_{n}$

**In Practice**: Unstable for bigger step sizes

Solve recursion: 
$$
\begin{align}
y_{n+1} &= y_{n} + h\lambda y_{n} \\
&= (1 + h\lambda) y_{n} \\
&= (1 + h\lambda)^{2} y_{n-1} \\
&= \ldots \\
&= (1 + h\lambda)^{n} y_{1}
\end{align}
$$
Stability Condition: For $|(1+h\lambda)^{n} y_{1}| < \infty$, we need $|(1 + h\lambda)| < 1$.
(Recall: Damped system $\Rightarrow$ $\lambda < 0$)

Especially bad for [[Stiff Problem]]s.
#### Implicit Euler
[[Solving ODEs#Implicit Euler]]
Implicit Euler Update: $y_{n+1} = y_{n} + h \lambda y_{n+1}$

**In Practice**: Stable, but shrinks too fast

Solve recursion:
$$
\begin{align}
y_{n+1} &= y_{n} + h\lambda y_{n+1} \\
&= (1 - h\lambda)^{-1} y_{n} \\
&= (1 - h\lambda)^{-2} y_{n-1} \\
&= \ldots \\
&= (1 - h\lambda)^{-n} y_{1}
\end{align}
$$
Stability Condition: For $|(1 - h\lambda)^{-n} y_{1}| < \infty$, we need $|(1 - h\lambda)^{-1}| < 1$.
Since $\lambda < 0, h > 0$, we have $h\lambda < 0 \Rightarrow 1-h\lambda > 1$, always stable.

**Implicit Euler is unconditionally stable** for linear ODEs and $\lambda < 0$, damped systems.
