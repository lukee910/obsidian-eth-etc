![[Hookean Springs Setup.png]]
* $L$ length undeformed
* $l$ length deformed
* $k$ spring stiffness
* $f^{int}$ internal force (spring pulling back)
* $f^{ext}$ external force (force applied to spring)
## Elastic Springs
For elastic springs, forces are [[Conservative Force|conservative]].
## Work
$$
\begin{align}
W &= \int_{L}^{l} f_{ext}(x) dx \\
&= \int_{L}^{l} -f_{int}(x) dx \quad \text{(conservative)} \\
&= \int_{L}^{l} k(x-L) dx
\end{align}
$$
Stored energy of the spring is:
$$
E(l) = W(l)  = \int_{L}^{l} f^{ext}(x) dx = \frac{1}{2}k(l-L)^2
$$
Note:
$$
\begin{align}
E(l) &= E(L) + \int_{L}^{l} \frac{dE}{dx}(x) dx = \int_{L}^{l}-f^{int}(x) dx \\
f^{int} &= -\frac{dE}{dx} = -k(l - L)
\end{align}
$$
### Work In $R^n$
Spring between points $x_{1}, x_{2}$, $e = x_{2}-x_{1}$. Force on $x_{1}$:
$$
\begin{align}
f_{1} &= -\frac{\partial E(x_{1}, x_{2})}{\partial x_{1}} \\
\frac{\partial E}{\partial l} &= k(l-L) \\
\frac{\partial l}{\partial x_{1}} &= \frac{1}{2} (e^{T}e)^{-\frac{1}{2}} \frac{\partial(e^{T}e)}{\partial x_{1}}
\end{align}
$$

So we get the force on $x_1$ and $x_2$:
$$
\begin{align}
f_{1} &= k(l-L) \frac{x_{2}-x_{1}}{|x_{2} - x_{1}|} \\
f_{2} &= -f_{1}
\end{align}
$$
## Spring Network
![[Spring Network.png]]

* $E$ Energy
	* $E  = \sum_{k} E_{k}$
* $f_{i}^{int}$ Spring force at node $i$
	* $f_{i}^{int} = -\frac{\partial E}{\partial x} = -\sum_{k} \frac{\partial E_k}{\partial x_i}$
* $f_{i}$ Total force at node $i$
	* $f_{i} = f_{i}^{int} + f_{i}^{ext}$



