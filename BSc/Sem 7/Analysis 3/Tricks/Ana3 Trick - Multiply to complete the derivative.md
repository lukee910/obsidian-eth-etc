## Trick

If you have a PDE term, e.g. $u_x$, multiply something to enable writing it as $\frac{\delta}{\delta x}$ instead.

## Example

$$
\begin{align*}
	& u_x(x, y) = c_0 u(x,y) + c_1 (x, y) \\
	\Leftrightarrow &\ [u_x(x, y) - c_0 u(x,y)] e^{-c_0x} = c_1 (x, y) e^{-c_0x} & | \cdot e^{-c_0x} \\
	\Leftrightarrow &\ u_x(x, y) e^{-c_0x} - c_0 u(x,y) e^{-c_0x} = c_1 (x, y) e^{-c_0x} \\
	\Leftrightarrow &\ \frac{\delta}{\delta x} \left( u(x,y)e^{-c_0x} \right) = c_1 (x, y) e^{-c_0x}
\end{align*}
$$
From there, integrate on both sides and divide by $e^{-c_0x}$ to get a solution for $u(x,y)$.