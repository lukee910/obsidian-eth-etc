Goal: Evaluate any integral, no matter of the dimensionality.

## Las Vegas vs Monte Carlo
* Las Vegas: Always correct, time random
* Monte Carlo: Always fast, error random
## Monte Carlo Integration Setting
Need:
* Method to pick random sample in domain (sampling)
* Being able to evaluate the integrand
Pros:
- Works for arbitrary integrands and dimensions
- Easy to extend with more sophisticated sampling
Cons:
- Noise from stochastics

See: [[Probability Recap]]
## Monte Carlo Summary
See: [[Monte Carlo Estimator]]
$$
\begin{align}
\int_{D} f(x)\ dx &= \int_{D} \left[ \frac{f(x)}{p(x)} \right] p(x)\ dx \\
&\approx \frac{1}{N} \sum\limits_{i=1}^{N f\frac{x_{i}}{p(x_{i})}} = F_{N}
\end{align}
$$
- Goal: Evaluate Integral $\int_{a}^{b} f(x) dx$
- Random Variable: $X_{i} \sim p(x)$
- [[Monte Carlo Estimator]] $F_{N}$
- Expectation: $E[F_{N}] = \int_{a}^{b} f(x) dx$
## Implementation
```c
double integrate(int N)
{
	double x, sum=0.0;
	for (int i = 0; i < N; i++)
	{
		x = drand48(); // p(x_i) = 1
		sum += exp(sin(3 * x * x)); // evaluate integrand
	}
	return sum / double(N);
}
```

Adding bounds:
```c
double integrate(int N, double a, double b)
{
	double x, sum=0.0;
	for (int i = 0; i < N; i++)
	{
		x = drand48()*(b-a); // p(x_i) = 1/(b-a)
		sum += exp(sin(3 * x * x)); // evaluate integrand
	}
	return sum / double(N) * (b-a); // (b-a) = 1/p(x_i), divide by PDF
}
```
## Properties
* [[Unbiased Estimators]]
	* Expected value equals integral
* Higher dimension extension straight forward
* Convergence: $\mathcal{O}(\frac{1}{\sqrt{N}})$
	* Reduce the error by 2: 4 times as many samples
## Sampling Random Variables
For more complex domains, like spheres, hemispheres, squares, ...
### Example: Uniformly Sampling a Disk
[[Probability Density Function|PDF]]: Uniform probability density on unit disk
$$
p(x,y) = \begin{cases}
\frac{1}{\pi} & x^{2} + y^{2} < 1 \text{ (on disk)} \\ \\
0 & \text{otherwise}
\end{cases}
$$
Corresponding to:
$$
p(r, \phi) = \begin{cases}
\frac{r}{\pi} & r < R \text{ (on disk)} \\ \\
0 & \text{otherwise}
\end{cases}
$$
Goal: Draw samples distributed as: $(X_{i}, Y_{i}) \sim p(x, y)$
Problem: Pseudo random number generators give us only canonical uniform distribution.
### Rejection Sampling
![[Rejection Sampling]]
## Importance Sampling
We are trying to integrate $\int f(x) dx$ with our estimator $F_{N} = \frac{1}{N} \sum\limits_{i=1}^{N} \frac{f(X_{i})}{p(X_{i})}$ ([[Monte Carlo Estimator#Formula]]).

If we get a probability function $p(x)$ that is a constant factor of our target $f(x)$, i.e.:
$$
p(x) = c f(x) \quad (a)
$$
Then we get the following simplification:

$$
\begin{align}
\int p(x) dx = 1 \rightarrow c = \frac{1}{\int f(x) dx}
\end{align} \quad (b)
$$
Apply this to our estimator:
$$
\frac{f(X_{i})}{p(X_{i})} \stackrel{(a), \text{ rearr.}}{=} \frac{1}{c} \stackrel{(b)}{=} \int f(x) dx
$$
Then we get a estimator of zero variance. #Unclear : Exact formulation and application after this, since this is all looking very constant now.

Usually it's not possible to exactly cancel out the PDF. Even matching the shape roughly is much better!

Common strategy: Sample proportional to the integrand (or on one term of the integrand).
### Sampling Arbitrary Distributions
Idea: Get a random variable $X_{i}$ for the desired distribution based on a simple [[Uniform Random Variable]] $\xi$.
#### Inversion Method Process
[[_T Sampling Recipe]] Inversion Method

1. If you have two variables: Compute the individual probabilities
	1. E.g. if given $p(\theta, \phi)$, get $p(\theta)$ by integrating over $\phi$ and $p(\phi) = \frac{p(\theta, \phi)}{p(\theta)}$
2. Compute the [[Cumulative Distribution Function|CDF]] $P(x) = \int^{x}_{0} p(x')\ dx'$
	1. Antiderivative of wished for $p(x)$
3. Compute inverse $P^{-1}(x)$
4. Compute $X_{i}$
	1. Obtain [[Uniform Random Variable]] $\xi$
	2. Compute $X_{i} = P^{-1}(\xi)$
	3. Alternatively: $\xi = P(x) \Rightarrow x = P^{-1}(\xi)$
![[Inversion Method.png]]
#### Jacobian Method
[[_T Sampling Recipe]] Jacobian Method

Given: n-dimensional random variable $X_{i} \sim p_{x}(X)$
Goal: Distribution $p_{y}(Y_{i})$ of $Y_{i} = T(X_{i})$, where $T$ is some transformation.

Note: This chapter uses a lot of substitutions. For example, substituting $x = T^{-1}(z)$. 
##### General Case
Optional: Find $X_{i} = T^{-1}(Y_{i})$
New density is:
$$
p_{y}(y) = p_{y}(T(x)) = \frac{p_{x}(x)}{|J_{T}(x)|} = p_{x}(X) \cdot \left| J_{T^{-1}}(y) \right|
$$

Idea: Jacobian determinant describes local stretching of $T$. It is a local, linear approximation of $T$.
See [[#Linear Map]] example for how this works.
##### 1-D
(From exercise sheet 2 solution: [[CG Sheet 2#3.1 Jacobian Method]])
1. Find the inverse transformation: $x = T_{Z}^{-1}(z)$
2. Differentiate the inverse transformation to find $\frac{dx}{dz}$
   Note: $\frac{dx}{dz} = \frac{d}{dz} T_{Z}^{-1}(z)$
3. Use the Jacobian formula for transformation of variables:
   $$p_{Z}(z) = p_{X}(x) \left| \frac{dx}{dz} \right| = p_{X}(x) \left| \frac{d}{dz} T_{Z}^{-1}(z) \right|$$
   where $p_{X}(x)$ is the PDF of $X$
### Area-Preserving Sampling
[[Area-Preserving Sampling]]
### Sampling Examples
#### Linear Map $p(y) = 2y$
[[#Sampling Arbitrary Distributions]]

Goal: $p(y) = 2y$.
- [[Cumulative Distribution Function|CDF]] via antiderivative: $P(y) = y^{2}$
- $P^{-1}(y) = \sqrt{y}$
- Apply $P^{-1}$ pattern to target $Y_{i}$ and [[Uniform Random Variable]] $X_{i}$:
	- $Y_{i} = \sqrt{X_{i}}$
- Confirm [[Probability Density Function|PDF]] with $p_{y}(y) = p_{y}(T(x)) = \frac{p_{x}(x)}{|J_{T}(x)|}$:
	- #Unclear What is happening here?
	- $p(x) = 1$, $Y = \sqrt{X}$
	- $|J_{T}(x)| = |\frac{dy}{dx}| = \frac{1}{2\sqrt{x}}$
	- $p(y) = 2 \sqrt{x} = 2y$
#### 2D Distribution
Draw samples $(X, Y)$ from a 2D distribution $p(x, y)$

If $p(x,y)$ is [[Separable (Probability)|separable]], i.e. $p(x, y) = p_{x}(x) p_{y}(y)$, independently sample.

Otherwise, compute [[Marginal Density]]:
$$
p(x) = \int p(x, y)\ dy
$$
And the [[Conditional Density]]:
$$
p(y|x) = \frac{p(x, y)}{p(x)}
$$

Procedure: First sample $X_{i} \sim p(x)$, then $Y_{i} \sim p(y|x)$.
#### Uniform Sampling of a Disk
[[Uniform Sampling of a Disk]]
#### Direct Sphere Sampling
[[Directly Sampling a Sphere]]
#### Cosine-Weighted Hemispherical Sampling
Turns out: Generating points uniformly on the disc and then projecting these points to the surface of the hemisphere produces the desired distribution.
![[Cosine-weighted Hemisphere Sampling.png]]
#### Triangles
#TODO: Triangle sampling
#### Various Distributions
#TODO: Insert screenshot from page 108 source
## Ambient Occlusion
Setup: Diffuse objects, illuminated by ambient white sky.
Simplified rendering function:
$$
l_{r}(x) = \frac{\rho}{\pi} \int_{H^{2}} V(x, \vec{\omega_{i}}) \cos \theta_{i}\ d\vec{\omega_{i}}
$$
Monte Carlo-ify:
![[Ambient Occlusion Setup.png]]
Note: For the result on slide 69: Uniform sampling can generate varied values, cosine sampling only gets ${0,1}$. That's why there are white values in the top image.

#TODO: Slide 77
## More Integration Dimensions
* Anti-aliasing (image space)
* Light visibility (surface of area lights)
* Depth-of-field (camera aperture)
* Motion blur (time)
* Many lights
* Multiple bounces of light
* Participating media (volume)
## Low Discrepancy Sampling
e.g. Stratified Sampling