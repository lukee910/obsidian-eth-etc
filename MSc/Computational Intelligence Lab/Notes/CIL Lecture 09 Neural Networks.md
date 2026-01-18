Learning an unknown vecture-valued function or map: $\Psi : \mathbb{R}^n \to \mathbb{R}^p$ or function $\psi : \mathbb{R}^n \to \mathbb{R}$.

Supervised learning: Training data set $S = \{ (x_t, y_t) \}$.

Deep learning: Deep series of maps, all of them changeable. No handcrafted features, generally.

$\psi = g \circ H_L \circ H_{L-1} \circ \ldots \circ H_1$, $H_l : \mathbb{R}^{n_{l-1}} \to \mathbb{R}^{n_l}$.
$g$ linear map.

-> Increasing amount of meaning over the intermediate representations from the layers.

## Composition of Linear Maps

![[Deep Learning Linear Maps.png]]

Ridge Functions: Linear + non-linear

$H = \Phi \circ F$, $H(x;\Theta) = \Phi(\Theta x)$.

By non-linearity on scalars:
$\Phi(z) = \left( \phi(z_1) \ldots \phi(z_m) \right)^T$, $\phi : \mathbb{R} \to \mathbb{R}$.

ReLU: $(z)_+ = \max(0,z)$.
**Sigmoid**: $\sigma(z) = \frac{1}{1 + e^{-z}}$. ([[Remember for Exam]])
$\tanh(z) = \frac{e^z - e^{-z}}{e^z + e^{-z}} = 2\sigma(2z) - 1$. -> Similar to $\sigma$, but has negative values.

Note: ReLU not differentiable at 0, can use Softplus or GELU instead (especially GELU).

## Multilayer Perceptron

![[Single Layer MLP Def.png]]

($\beta$ are linear map factors)

### Loss and derivations
![[MLP Derviatives.png]]

$\sigma'(z) = \sigma(z)(1 - \sigma(z)) = \sigma(z)\sigma(-z)$.

### Stochastic Gradient Descent
Stochastic: Don't use full data, just update on minibatch.

1. Sample random minibatch $S_t$ from training data
2. Calculate all partial derivatives, see before: $$
   \Delta_\vartheta(\beta, \Theta; S_t) := \sum_{(x,y) \in S_t} \frac{\partial \frac{1}{2}(\psi(x;\beta,\Theta) - y)^2}{\partial\vartheta},\quad \vartheta \in \{ \beta_j, \theta_{ji} \}
$$
3. Update: $\vartheta_{t+1} = \vartheta_t - \eta \Delta_\vartheta (\beta, \Theta; S_t)$. $\eta$ learning rate / step size.

## Backpropagation

Exploit compositionality for gradients.

For a single unit: $h = \phi(<\theta, z>)$.
**Error signal (aka delta)**:
$$
\delta := \frac{\partial l}{\partial h}
$$
Delta quantifies how much the loss changes if activation $h$ is changed.

=> Parameter gradients by chain rule:
$$
\nabla_{\theta}\ell=\frac{\partial\ell}{\partial h}~\nabla_{\theta}h=\delta~\phi^{\prime}(\langle\theta,\mathbf{z}\rangle)~\mathbf{z}
$$
where $z$ is the input to the unit (i.e. previous layer activation).

Everything but the Delta can be calculated on the forward path.

### Jacobi Matrix / Map
For H the map of activations:
$$
H:\mathbb{R}^{n}\to\mathbb{R}^{m},\quad H(\mathbf{z})=\left(\begin{array}{l}{{h_{1}(\mathbf{z})}}\\ {{\ldots}}\\ {{h_{m}(\mathbf{z})}}\end{array}\right)
$$
**Jacobi Map** is:
$$
[{\bf J}_{H}]_{i j}:=\frac{\partial h_{i}}{\partial z_{j}}
$$
Jacobi Matrix: $J_H(z)$, with a concrete value.
=> $H(z+\Delta z)\approx H(z)+J_{H}(z)\Delta z$

![[Backpropagation Recurrence.png]]

**Jacobi matrix** depends on **activations** (forward).
**Delta** depends on backwards prop data.

### Delta

For squared loss:
$$\ell({\bf x},{\bf y})=\frac{1}{2}({\bf y}-\Psi({\bf x}))^{2},\quad\delta_{L}=\frac{\partial\ell}{\partial H_{L}}=\Psi({\bf x})-{\bf y}\,,$$
For logistic loss: $y \in \{ -1, 1 \}$, $n_L = 1$
$$
\ell({\bf x},y)=-\ln\sigma(y\psi({\bf x})),\;\;\;\;\delta_{L}=\frac{\partial\ell}{\partial h_{L}}=-y\,\sigma(-y\psi({\bf x}))
$$
### Algorithm
1. Forward pass, compute $z_1, \ldots, z_L$
2. Calculate loss-specific error $\delta_L$
3. Backpropagate via Jacobi-vector products to obtain $\delta_{L-1},\ldots,\delta_1$
4. Calculate partial derivatives, accumulate
5. Perform minibatch SGD update

## Gradient Methods

Convergence?

((omitted from notes))

Optimal step size:
$$
\eta* = \frac{2}{\lambda_{\max} + \lambda_{\min}}
$$
