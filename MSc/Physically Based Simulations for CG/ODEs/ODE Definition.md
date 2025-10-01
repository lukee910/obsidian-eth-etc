## Differential Equations
Equations describing a function through its derivatives.
E.g. $\dot{y} = \frac{dy}{dt} = ay$.
### Order
Order of a differential equation is the order of the highest derivative (e.g. $\dot{y} = \frac{dy}{dt} = ay$ has order 1).
## ODEs
Differential Equations with respect to a single variable $t$:
$$
y^{(n)} = f(t, y, y', \ldots, y^{(n-1)})
$$
## Initial Value Problem
ODE + initial condition (the value of the unknown function at a certain point, e.g. $y(0) = C$).

These problems are uniquely solvable if they are Lipschitz-continuous (Picard-Lindelöf-Theorem) and also often otherwise.
## Higher Order ODE
E.g. Newton's second law:
$$
\ddot{x_{i}} = f_{i}(t, x_{i}) / m_{i}
$$
Can be broken apart into multiple first order ODEs for steps:
$$
\begin{align}
\dot{x_{i}} &= v_{i} \\
\dot{v_{i}} &= f_{i}(t, x_{i}) / m_{i}
\end{align}
$$
Equivalently:
$$
\frac{d}{dt} \begin{bmatrix}
x_{i} \\ v_{i}
\end{bmatrix} = \begin{bmatrix}
v_{i} \\ f_{i} / m_{i}
\end{bmatrix}
$$
Introduce a state vector with $x_{i}, v_{i}$: $y_{i} = (x_{i}, v_{i})^T$. Then we get a single ODE:
$$
y' = f(t, y)
$$
