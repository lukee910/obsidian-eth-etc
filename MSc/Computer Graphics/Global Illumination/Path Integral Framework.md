## Path Integral Form of Measurement Equation
In surface terms:
$$
I_{j} = \int_{A} \int_{A} W_{e}(x_{0}, x_{1}) G(x_{0}, x_{1}) L_{o}(x_{0}, x_{1})\ dx_{1}\ dx_{0}
$$
Unfold the recursion:
#TODO: Slide 9

Which breaks down into components:
#TODO: Slide 10

$\Rightarrow$ Fancy way of writing down: Take importance at first one, emission at the last one, importance in between.

#TODO: Simplifications slides 11-12
## Overview
#TODO: Overview slide 14
## Monte Carlo Estimator
$$
I_{j} \approx \frac{1}{N}\sum^{N}_{i=1}\frac{W_{e}(x_{i,0}, x_{i,1}) L_{e}(x_{i,k}, x_{i,k-1}) T(\bar{x}_{i})}{p(\bar{x}_{i})}
$$
## Importance Sampling
### Path Tracing
To construct the path probability, follow along and calculate probabilities as you go:
$$
\begin{align}
p(\bar{x}) &= p(x_{0}) \\
&\times p(x_{1} | x_{0}) \\
&\times p(x_{2} | x_{0}x_{1}) \\
&\times \ldots
\end{align}
$$
### Path Tracing with NEE
$$
\begin{align}
p(\bar{x}) &= p(x_{0}) \\
&\times p(x_{1} | x_{0}) \\
&\times p(x_{2} | x_{0}x_{1}) \\
&\times p(x_{3})
\end{align}
$$
Where $x_{3}$ hits the light, manual emitter sampling.
By assuming uniform area sampling.
### Light Tracing
Guess what, flip it again.
$$
\begin{align}
p(\bar{x}) &= p(x_{0} | x_{3}x_{2}x_{1}) \\
&\times p(x_{1} | x_{3}x_{2}) \\
&\times p(x_{2} | x_{3}) \\
&\times p(x_{3})
\end{align}
$$
But without NEE this doesn't make sense with pinhole cameras.
### Light Tracing with NEE
$$
\begin{align}
p(\bar{x}) &= p(x_{0}) \\
&\times p(x_{1} | x_{3}x_{2}) \\
&\times p(x_{2} | x_{3}) \\
&\times p(x_{3})
\end{align}
$$
By assuming uniform aperture sampling.
### Uniform sampling of surfaces
Technically, something like this also works:
$$
\begin{align}
p(\bar{x}) &= p(x_{0}) \\
&\times p(x_{1}) \\
&\times p(x_{2}) \\
&\times p(x_{3})
\end{align}
$$
It's gonna be horrible though, chance of getting an important path is basically 0.
