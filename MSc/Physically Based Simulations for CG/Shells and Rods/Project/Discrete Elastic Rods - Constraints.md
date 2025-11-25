Variables for the code. May be incorrect.

In code, `x_lambda` = $x_{\lambda} \in \mathbb{R}^{n+2}$ in `constraints.cpp` ($\leftrightarrow$ `y` in `Optimization.h`) are the adjusted vertex positions.
## Stretch / Inextensibility
### Energy and $C$
Start with the energy:
$$
E_s^i = 1/2 (|x_{i+1} - x_i| - |\bar{e^i}|)^2
$$
$C_{Stretch} \in n+1$ stretch constraint values:
$$
\begin{align}
	C_{Stretch} &= E_{s}\\
	C^{|i|} &= C_{Stretch_{i}} & \text{Shorthand for edge length constraint per edge}
\end{align}
$$
### Gradient
Get the gradient $\nabla_{i} C$ for each adjusted position $x_{\lambda,i}$ of $x_{\lambda}$. Note the dimension of $\nabla C \in \mathbb{R}^{3 \times n+2}$, or in code `C`$\in \mathbb{R}^{3\cdot(n+2)}$ as a block vector. #Unclear: Are the dimensions correct? Do we need the Jacobian or gradient, what's the detailed difference here?

In Parts:
Contribution for following edge $e^{i}$ on $i <= n$:
$$
\begin{align}
\nabla_{i} C^{|i|} &= \nabla_{i} \left( \frac{1}{2} (|x_{\lambda,i+1} - x_{\lambda,i}| - |\bar{e}^{i}|)^{2} \right) \\
&= \left( |x_{\lambda,i+1} - x_{\lambda,i}| - |\bar{e}^{i}| \right) \cdot \frac{x_{\lambda,i+1} - x_{\lambda,i}}{|x_{\lambda,i+1} - x_{\lambda,i}|}
\end{align}
$$
Contribution for leading edge $e^{i-1}$ on $i > 0$:
$$
\begin{align}
\nabla_{i} C^{|i-1|} &= \nabla_{i} \left( \frac{1}{2} (|x_{\lambda,i} - x_{\lambda,i-1}| - |\bar{e}^{i-1}|)^{2} \right) \\
&= \left( |x_{\lambda,i} - x_{\lambda,i-1}| - |\bar{e}^{i-1}| \right) \cdot \frac{x_{\lambda,i} - x_{\lambda,i-1}}{|x_{\lambda,i} - x_{\lambda,i-1}|}
\end{align}
$$
Total stretch gradient for $x_{i}$:
$$
\nabla_{i} C_{Stretch} = \nabla_{i} C^{|i|} + \nabla_{i} C^{|i-1|}
$$
### Hessian
$x_{\lambda,i}$ is contained in $\nabla_{j} C_{Stretch}$ for $j \in i-1, i, i+1$. Otherwise derives to 0. We get a band diagonal $H_{C_{Stretch}}$.

For calculations see Maple.
## End Clamping
TODO: Add some end clamping constraint $C_{Ends}$ etc.f
## Combining Constraints
Combine all constraints into one. Add to here whenever we get around to doing this:
$$
C = \begin{bmatrix}
C_{Stretch} \\ ...
\end{bmatrix}
$$