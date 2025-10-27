## 2. Time Integration
### Analytical Solution
$$
\begin{align}
y(t) &= c_{1} e^{\alpha t} \cos(\beta t) + c_{2}e^{\alpha t}\sin(\beta t) - L_{0} - m\frac{g}{k} \\
\alpha &= -\frac{\gamma}{2m},\quad \beta = \frac{\sqrt{4km-\gamma^{2}}}{2m}
\end{align}
$$
Task: Figure out $c_{1}, c_{2}$.

Initial Conditions:
* $y(0) = (p_{0})_{y} - L_{0}$
* $y'(0) = 0$

$y'$:
$$
\begin{align}
y'(t) &= c_{1} \alpha e^{\alpha t} \cdot \cos(\beta t) + c_{1} e^{\alpha t} \cdot \cos'(\beta t) \\
&\quad + c_{2} \alpha e^{\alpha t} \cdot \sin(\beta t) + c_{2} e^{\alpha t} \cdot \sin'(\beta t) - 0 \quad \text{Product Rule} \\
&= c_{1} \alpha e^{\alpha t} \cdot \cos(\beta t) + c_{1} e^{\alpha t} \cdot (-\sin(\beta t) \cdot \beta) \\
&\quad + c_{2} \alpha e^{\alpha t} \cdot \sin(\beta t) + c_{2} e^{\alpha t} \cdot \cos(\beta t) \cdot \beta \quad \text{Chain Rule} \\
&= c_{1} e^{\alpha t} \left(\alpha \cos(\beta t) - \beta \sin(\beta t)\right) + c_{2} e^{\alpha t} \left(\alpha \sin(\beta t) + \beta \cos(\beta t)\right)
\end{align}
$$
#### Condition 2, $y'(0)$:
$$
\begin{align}
y'(0) &= c_{1} e^{\alpha 0} \left(\alpha \cos(\beta 0) - \beta \sin(\beta 0)\right) + c_{2} e^{\alpha 0} \left(\alpha \sin(\beta 0) + \beta \cos(\beta 0)\right) \\
&= c_{1} \cdot 1 \left(\alpha \cdot 1 - 0 \right) + c_{2} \cdot 1 \left(\alpha \cdot 0 + \beta \cdot 1 \right) \\
&= c_{1} \cdot \alpha + c_{2} \cdot \beta \\
&\stackrel{!}{=} 0 \\
&\Rightarrow c_{2} = -c_{1} \cdot \frac{\alpha}{\beta}
\end{align}
$$
#### Condition 1: $y(0) = (p_{0})_{y} - L_{0}$:
$$
\begin{align}
y(0) &= c_{1} e^{\alpha 0} \cos(\beta 0) + c_{2}e^{\alpha 0}\sin(\beta 0) - L_{0} - m\frac{g}{k} \\
&= c_{1} \cdot 1 \cdot 1 + c_{2} \cdot 1 \cdot 0 - L_{0} - m\frac{g}{k} \\
&= c_{1} - L_{0} - m\frac{g}{k} \\
&\stackrel{!}{=} (p_{0})_{y} - L_{0}
\end{align}
$$
$\Rightarrow$
$$
\begin{align}
c_{1} - L_{0} - m\frac{g}{k} &= (p_{0})_{y} - L_{0} \\
\Rightarrow c_{1} = (p_{0})_{y} + m\frac{g}{k}
\end{align}
$$



