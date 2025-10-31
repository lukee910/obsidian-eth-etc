## Constraint
[[Constraint]]
$C(x_{0}, x_{1}) = |x_{1} - x_{0}| - L$
## Penalty Force
[[Penalty Force]]
$$
\begin{align}
F_{1}^{C}(x_{0}, x_{1}) &= -kC(x_{0}, x_{1}) \frac{\partial C(x_{0}, x_{1})}{\partial x_{1}} \\
&= -k(|x_{1} - x_{0}| - L) \frac{x_{1} - x_{0}}{|x_{1} - x_{0}|}
\end{align}
$$
Note: This is the spring force! See [[Hookean Springs#Work in $R n$]].
## Time Stepping
[[Solving ODEs#Explicit Euler]] (not recommended in general):
$$
v_{n+1} = v_{n} + hM^{-1}(F^{C}(x) + F^{ext})
$$
