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
Goal: Draw samples distributed as: $(X_{i}, Y_{i}) \sim p(x, y)$
Problem: Pseudo random number generators give us only canonical uniform distribution.
### Rejection Sampling
#### Disk
```c
Vec2 v;
do {
	// sample
	v.x = 1 - 2 * drand48();
	v.y = 1 - 2 * drand48();
// while sample invalid
} while (v.length() * v.length() > 1)
```
#### Sphere
```c
Vec3 v;
do {
	// sample
	v.x = 1 - 2 * drand48();
	v.y = 1 - 2 * drand48();
	v.z = 1 - 2 * drand48();
// while sample invalid
} while (v.length() * v.length() > 1)
// Project onto sphere surface
v /= v.length();
```
Note: For hemisphere, sample sphere and then flip on appropriate axis if it's in the wrong hemisphere.
#### Properties
Pros:
- Flexible
Cons:
- Inefficient
- Problems with low-discrepancy sampling

Used for: Complex shapes. If you have an analytical solution (See [[CG 04V2 Monte Carlo#Inversion Method Process]]), use that.
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

#TODO: Something's not entirely right here. How to use this for exercise [[CG Sheet 2#3.1 Jacobian Method]]?
#### Inversion Method Process
1. Compute the CDF $P(x) = \int^{x}_{0} p(x')\ dx$
	1. Antiderivative of wished for $p(x)$
2. Compute inverse $P^{-1}(x)$
3. Obtain [[Uniform Random Variable]] $\xi$
4. Compute $X_{i} = P^{-1}(\xi)$
![[Inversion Method.png]]
#### Transforming Between Distributions
Given: n-dimensional random variable $X_{i} \sim p_{x}(X)$
Goal: Distribution of $Y_{i} = T(X_{i})$, where $T$ is some transformation.

New density is:
$$
p_{y}(y) = p_{y}(T(x)) = \frac{p_{x}(x)}{|J_{T}(x)|}
$$

Idea: Jacobian determinant describes local stretching of $T$. It is a local, linear approximation of $T$.
See [[#Linear Map]] example for how this works.
### Sampling Examples
#### Linear Map
[[#Sampling Arbitrary Distributions]]

Goal: $p(y) = 2y$.
- [[Cumulative Distribution Function (CDF)|CDF]] via antiderivative: $P(y) = y^{2}$
- $P^{-1}(y) = \sqrt{y}$
- Apply $P^{-1}$ pattern to target $Y_{i}$ and [[Uniform Random Variable]] $X_{i}$:
	- $Y_{i} = \sqrt{X_{i}}$
- Confirm [[Probability Density Function|PDF]] with $p_{y}(y) = p_{y}(T(x)) = \frac{p_{x}(x)}{|J_{T}(x)|}$:
	- #Unclear What is happening here?
	- $p(x) = 1$, $Y = \sqrt{X}$
	- $|J_{T}(x)| = |\frac{dy}{dx}| = \frac{1}{2\sqrt{x}}$
	- $p(y) = 2 \sqrt{x} = 2y$
#### 2D Distribution
#TODO: 2D Distribution via marginal density
#### Uniform Sampling of a Disk
Note: Switch from $x,y$ to $r,\theta$: We start with x^2, y^2 in the formula, then we want to switch to polar. #TODO: This
#### Recipe
#TODO: Slide 98
#### Direct Sphere Sampling
#TODO: Slide 101
#### Simplified Direct Sphere Sampling
Improvement on slide 101 (green box) is based on Pythagorean theory, move the $\cos$ up and use $\sin = 1 - \cos^{2}$.

Alternative view of looking at it:
Use [[Archimedes' Hat-Box Theorem]]:
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