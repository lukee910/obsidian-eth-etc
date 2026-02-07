Adaption of [[Reflection Equation Importance Sampling]]
Motivation: [[Variance]] is high when the [[Probability Density Function|PDF]] is not proportional to the integrand (worst case: [[Fireflies (CG)|Fireflies]]).
## Formulations
### Multi-Sample Model
Weighted combination of $M$ strategies:
$$
<F^{\sum N_{s}}> = \sum\limits_{s=1}^{M} \frac{1}{N_{s}} \sum\limits_{i=1}^{N_{s}} \omega_{s}(x_{i}) \cdot \frac{f(x_{i})}{p_{s}(x_{i})}
$$
### One-Sample Model
Idea: Only sample once per estimate (like we do in [[Path Tracing]]):
$$
<F^{1}> = \omega_{s}(x) \frac{f(x)}{q_{s}p_{s}(x)}
$$
Where $q_{s}$ is the probability of using strategy $s$: $\sum_{s=1}^{N} q_{s} = 1$. From the [[#Multi-Sample Model]]:
$$q_{s} = \frac{N_{s}}{\sum_{j} N_{j}}$$

We get the estimator for $N$ samples, with each strategy being evaluated on each sample:
$$
<F^{N}> = \frac{1}{N} \sum\limits_{i=1}^{N} \frac{f(x_{i})}{\sum_{j} q_{j}p_{j}(x_{i})}
$$

Note: This works to reduce [[Fireflies (CG)|Fireflies]], since if the [[Probability Density Function|PDF]] of at least one strategy is large, the fraction will not explode as much as before.
## Weights
### Balance Heuristic
$$
\omega_{s}(x) = \frac{N_{s} p_{s}(x)}{\sum_{j} N_{j} p_{j}(x)}
$$
$\Rightarrow$ we will use this one.
### Power Heuristic
$$
\omega_{s}(x) = \frac{(N_{s} p_{s}(x))^{\beta}}{\sum_{j} (N_{j} p_{j}(x))^{\beta}}
$$
