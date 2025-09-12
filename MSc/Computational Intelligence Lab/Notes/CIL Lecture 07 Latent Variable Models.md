# Latent Variable Models
## Intro latent variables

X observables, Z latent variables. Each $x_t$ is a pattern.

For each $X_t$ we assume there to exist a latent variable $Z_t$ to exist, that we did not observe.

Complete data model: Model over both X and Z.

Marginal model: Only $p(X)$, complete marginalized (summed over) $p(Z)$

$k$ classes, not specified which. $Z_t \in \{ 1, \ldots, k \}$.

Each latent class variable $Z_t$ follows categorical law:
* $Z_t \sim^{iid} Categ(\pi_1, \ldots, \pi_k)$
* $\pi = (\pi_1, \ldots, \pi_k)$ prior probability per class
* $\pi \geq 0,\ \Sigma_z \pi_z = 1$
* $\mathbb{P}(Z_t = z) = \pi_z$
We want to discover these $Z_t$

Conditional distr. per class: $p(x|z) = p(x;\theta_z)$. $\theta_z$ parameter for probability family per category/component.

**Complete data model**: $p(x,z) = \pi_z p(x|z)$.

## Mixture Model via Marginalization

$\theta = (\pi, \theta_1, \ldots, \theta_k)$

Note: $p_z$ probability of class being $z$, $\theta_z$ is the distribution of that class.

=> $p(x;\theta) = \Sigma_{z=1}^k p(x, z) = \Sigma_{z=1}^k \pi_z p(x;\theta_z)$
Convex combination of class-specific distributions

## Latent Class Posteriors

$$
\mathbb{P}(Z = z | x; \theta) = \frac{\pi_z p(x;\theta_z)}{\Sigma_{\zeta=1}^k \pi_\zeta p(x;\theta_\zeta) = p(x;\theta)}
$$
From Bayes' rule

## Maximum Likelihood Estimation MLE

Likelihood:

$$
L(\theta; \{x_1,\ldots,x_s\}) = \Pi_{t=1}^s p(x_t;\theta) = \Pi_{t=1}^s \Sigma_{z=1}^k \pi_z p(x_t;\theta)
$$
But, we don't like products, so apply log:

Log-Likelihood:

$$
l(\theta; \{x_1,\ldots,x_s\}) = \Sigma_{t=1}^s \ln p(x_t;\theta) = \Sigma_{t=1}^s \ln \Sigma_{z=1}^k \pi_z p(x_t;\theta_z)
$$
$$\theta^{MLE} = \arg \max_\theta l(\theta; \{x_1, \ldots, x_s\})$$
Note: log of sum is not convex! => EM

## Expectation-Maximation Algorithm

Exploit Jensen's inequality: For any convex $\psi$ / concave $\phi$:
$$
	\psi(E[X]) \leq E[\psi(X)],\quad \phi(E[X]) \geq E[\phi(X)]
$$
Use $\phi = \ln$.

Variational Distribution:
$$
	q_z \geq 0 (z = 1,\ldots,k),\ \Sigma_z q_z = 1
$$
Introduce variational params $q_z$ into per-pattern log-likelihood:
$$
l(x; \theta) = \ln \Sigma_{z=1}^k \underline{q_z \frac{\pi_z}{q_z}} p(x;\theta_z)
$$
With this $= \ln E_q f(z) \geq E_q \ln f(z)$:
$$
	\geq \Sigma_{z=1}^k q_z \ln \left( \frac{\pi_z}{q_z} p(x;\theta_z) \right)
$$
(For any $q_z$)

Rewrite =>:
![[LogLikelihood with KL.png]]

With Kullback-Leibler divergence:
$$
	D_\text{KL}(P \parallel Q) = \sum_{ x \in \mathcal{X} } P(x) \, \ln \frac{ P(x) }{ Q(x) }\text{.}
$$
=> Maximize probability while minimizing the divergence between $q$ and $\pi$

This was on one pattern $x$. For more patterns, introduce: $q_{tz}$ for $x_t$.

**Evidence Lower Bound (ELBO)**
$$
\begin{align}
	l(\theta) &= \Sigma_{t=1}^s \ln \Sigma_{z=1}^k \pi_z p(x_t;\theta_z) \\
	&\geq \Sigma_{t=1}^s \Sigma_{z=1}^k q_{tz} [\ln \pi_Z + \ln p(x_t;\theta_z) - \ln q_{tz}]
\end{align}
$$
=Variational Lower Bound

Maximizing wrt $q$ increases tightness of bound
Maximizing wrt $\theta$ increases fit of bound

### E-Step
Fix $\theta$, maximize $q_{tz}$ per pattern $t$ (they are independent per pattern).

![[E-Step EM.png]]

$\sum_{z} q_z = 1$ with Lagrange multiplier

### M-Step
First, find the optimal mixing proportions $\pi_z$.

![[M-Step EM.png]]

Note: $\lambda = s$

Then, optimize $\theta_z$. Q: What distribution?

Popular choice: Gaussian Mixture Model, because Center Limit Theorem (everything goes gaussian on the sample mean with enough samples)

![[M-Step EM for Gaussian.png]]
