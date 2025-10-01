$\dot{x} = v(t) \quad \dot{v} = f(t, x(t)) / m$

## Explicit Euler
[[Solving ODEs#Explicit Euler]]
$$
\begin{align}
x_{n+1} &= x_{n} + hv_{n} \\
v_{n+1} &= v_{n} + hf(x_{n}) / m
\end{align}
$$
Note: Velocity and position updated separately
