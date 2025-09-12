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

1. Sample random minibatch $S_t$ from training data
2. Calculate all partial derivatives, see before: $$
   \Delta_\vartheta(\beta, \Theta; S_t) := \sum_{(x,y) \in S_t} \frac{\partial \frac{1}{2}(\psi(x;\beta,\Theta) - y)^2}{\partial\vartheta},\quad \vartheta \in \{ \beta_j, \theta_{ji} \}
$$
3. Update: $\vartheta_{t+1} = \vartheta_t - \eta \Delta_\vartheta (\beta, \Theta; S_t)$. $\eta$ learning rate / step size.

