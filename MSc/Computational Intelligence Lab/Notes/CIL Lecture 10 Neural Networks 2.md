## Smoothness

$l:\mathbb{R}^d \to \mathbb{R}$ is $L$-smooth for some $L > 0$ if:
$$
\|\nabla\ell(\theta)-\nabla\ell(\theta^{\prime})\|\leq L\|\theta-\theta^{\prime}\|\quad(\forall\theta,\,\theta^{\prime})
$$
Lower L-smoothness => smaller changes of the gradient, smaller changes of loss.

Smoothness of $\ell$ $\Leftrightarrow$ Lipschitz continuity of $\nabla\ell$

**Lipschitz continuous**:
A function $f$ is Lipschitz continuous if $\exists L \geq 0$ s.t.
$$
|f(x)-f(y)|\leq L\|x-y\|\quad\forall x,y\in\mathbb{R}^{n}
$$
=> Slope is bounded

((derivations omitted))

For **gradient descent**: $\theta' = \theta - \eta \nabla \ell(\theta)$
$$
\ell(\theta^{\prime})-\ell(\theta)\leq-\eta\left(1-{\frac{L\eta}{2}}\right)\|\nabla\ell(\theta)\|^{2}
$$
=> Loss will reduce with $\eta$ small enough (from $1 - \frac{L\eta}{2}$).
With $\eta = 1/L$:
$$
\ell(\theta^{\prime})-\ell(\theta)\leq - \frac{1}{2L}\|\nabla \ell(\theta) \|^2
$$
Small L => large steps
Small $\|\nabla\ell(\theta)\|$ => small steps!

$\epsilon$-critical point: $\|\nabla\ell(\theta) \leq \epsilon\|$.

((some stuff omitted, steps count calculation))

### Conclusion

Smoothness is sufficient to find $\epsilon$-critical points with $\mathcal{O}(\epsilon^{-2})$ steps in gradient descent. (Or: L-smooth, then $\mathcal{O}(L\epsilon^{-2}$).

## Convergence
### Polyak-Lojasiewicz Condition (PL Condition)

A differentiable function $\ell$ obeys the Polyak-Lojasiewicz Condition with parameter $\mu > 0$, if and only if
$$
\frac{1}{2}||\nabla\ell(\theta)||^{2}\geq\mu\,(\ell(\theta)-\ell^{*})\;\;(\forall\theta),\quad\ell^{*}=\operatorname*{min}\ell(\theta)
$$
### Strong Convexity

A differentiable function $\ell$ is $\mu$-strongly convex, if it fulfils
$$
\ell(\theta^{\prime})\geq\ell(\theta)+\langle\nabla\ell(\theta),\theta^{\prime}-\theta\rangle+{\frac{\mu}{2}}\|\theta^{\prime}-\theta\|^{2}\quad(\forall\theta^{\prime},\,\theta)
$$
((convergence speed etc. omitted))

## Saddle Points

### Momentum and Acceleration

How to not get stuck? Add momentum!

### Heavy Ball Method (1964)
$$
\theta^{k+1}=\theta^{k}-\eta\nabla\ell(\theta^{k})+\beta\underbrace{(\theta^{k}-\theta^{k-1})}_{\mathrm{extrapolation}},\quad\beta\in(0;1)
$$
Accumulate momentum by re-applying a scaled down factor of the previous update.

Note: Large $\beta$ can lead to instability, usually hyperparameter tune.

### Momentum Method (1986)
Updated Heavy Ball

Idea: Incorporate moving average $v_k$ of past gradients.
$$
\begin{array}{c}{{v_{k+1}:=\beta v_{k}-\eta\nabla\ell(\theta_{k})}}\\ {{\theta_{k+1}:=\theta_{k}+v_{k+1}}}\end{array}
$$
Helps escape shallow regions, but also dampens oscillations.

### Nestrov Acceleration (1983)

Evaluates gradient at "momentum-extrapolated" point $\theta'$.
$$
\begin{array}{l c r}{{\theta^{\prime k+1}=\theta^{k}+\beta(\theta^{k}-\theta^{k-1}),}}\\ {{\theta^{k+1}=\theta^{\prime k+1}-\eta\nabla\ell(\theta^{\prime k+1})}}\end{array}
$$
Avoids overshooting.

### Adaptivity: AdaGrad (2011)

Prevent oscillations by setting step size per dimension.
Idea: Use history of gradients at previous iterates.

First, define $\gamma_{i}^{k}$, which accumulates energy / counts updates:
$$
\gamma_{i}^{k}=\gamma_{i}^{k-1}+\left[\partial_{i}\ell(\theta^{k})\right]^{2},\quad\partial_{i}\ell:=\frac{\partial\ell}{\partial\theta_{i}}
$$
Note: $\gamma_{i}^{k}$ always improves, if it's big, slow down learning rate to stabilize!

Adaptive step size update:
$$
\theta_{i}^{k+1}=\theta_{i}^{k}-\eta_{i}^{k}\ \partial_{i}\ell(\theta^{k}),\quad\eta_{i}^{k}:=\frac{\eta}{\sqrt{\gamma_{i}^{k}+\delta}}
$$
$\delta$ small constant for numerical stability, e.g. $10^{-8}$.

Problem: $\gamma_{i}^{k}$ may grow too much!

### RMSProp (2012)
Update to AdaGrad.

Instead, calculate $\gamma_{i}^{k}$ with exponential moving average:
$$
\gamma_{i}^{k}=\rho\gamma_{i}^{k-1}+(1-\rho)[\partial_{i}\ell(\theta^{k})]^{2}
$$
Typical decay rate $\rho = 0.9$.

### Adam (2014)
Updated RMSProp

Adaptive Momentum Estimation

$h_{i}^k$: Energy accumulated, like RMSProp
$g_{i}^{k}$: Apply momentum from previous step too
$$
\begin{array}{l l}{{g_{i}^{k}=\beta g_{i}^{k-1}+(1-\beta)\partial_{i}\ell(\theta^{k}),}}&{{\beta\in[0;1],}}&{{g_{i}^{0}:=\partial_{i}\ell(\theta^{0})}}\\ {{h_{i}^{k}=\alpha h_{i}^{k-1}+(1-\alpha)[\partial_{i}\ell(\theta^{k})]^{2},}}&{{\alpha\in[0;1],}}&{{h_{i}^{0}:=[\partial_{i}\ell(\theta^{0})]^{2}}}\end{array}
$$
Update rule:
$$
\theta_{i}^{k+1}=\theta_{i}^{k}-\eta_{i}^{k}g_{i}^{k},\quad\eta_{i}^{k}:=\frac{\eta}{\sqrt{h_{i}^{k}+\delta}}
$$
With typical values:
* $\beta = 0.9$
* $\alpha = 0.999$
* $\delta = 10^{-8}$
* $\eta = 10^{-3}$

## Convolutional Neural Networks

Motivation: Time signal $f : \mathbb{R} \to \mathbb{R}^m$. Transform to function $Tf : \mathbb{R} \to \mathbb{R}^m$ via operator $T$.

If our operator $T$ is linear, we can represent it via a (linear) kernel:

Given Kernel $H : \mathbb{R}^2 \to \mathbb{R}$ and an invterval $t_1, t_2 \in \mathbb{R} \cup \{ -\infty, \infty \}$, we can define an operator (assuming intergral exists) via:
$$
(Tf)(u) = \int_{t_{1}}^{t_{2}} H(u,t)f(t)dt
$$
If it's linear, we can do stuff like $T(f+g) = Tf + Tg$.

### Convolutions

**Shift-invariant operators**: Any linear shift-invariant operator can be represented as a **convolution**:
$$
(f * h)(u):=\int_{-\infty}^{\infty}h(u-t)f(t)\,d t=\int_{-\infty}^{\infty}f(u-t)h(t)\,d t
$$

Signals are digitally sampled => **discrete convolutions**:

1d:
$$
(f*h)[u]:=\sum_{t=-\infty}^{\infty}f[t]\,h[u-t]
$$
2d:
$$
(f*h)[x,y]:=\sum_{u=-\infty}^{\infty}\sum_{v=-\infty}^{\infty}\ f[u,v]\,h[x-u,y-v]
$$
(Rectangular brackets suggest arrays)

Examples:
* Gaussian Kernel: Smoothes out
* 1D edge detection, asymmetric kernel

Instead of having to flip the kernel for asymmetric ones, use **cross-correlation**: (sliding inner product)
$$
(h\star f)[u]:=\sum_{t=-\infty}^{\infty}h[t]\,f[u+t]
$$
Note $u + t$ vs convolution's $u-t$.
Note: Kernel is "flipped", cross correlation is equivalent to applying a convolution on the flipped kernel $\bar{h}$:
$$
(h\star f)=(\bar{h}\ast f),\quad\mathrm{where}\ \ \bar{h}[t]:=h[-t],
$$

### CNNs

Allows us to exploit locality.

Kernel weights $\theta_{i,(\delta_{x}, \delta_{y}, j)}$:
$j$: Input dimension
$i$: Output dimension
$\delta_{x},\ \delta_{y} \in \{ \ldots, -1, 0, 1, \ldots \}$: Position where we apply the kernel to the image
Outputs a vector of depth $k$ as a result of that kernel.



