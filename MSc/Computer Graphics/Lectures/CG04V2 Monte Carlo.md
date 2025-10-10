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
## Probability Recap
### Probability Densities
Continuous random variables use probability densities, since any given outcome has probability 0.
#### Cumulative Distribution Function (CDF)
$$
P(x) = Pr[X \leq x] \quad P(x) \in [0,1]
$$
#### Probability Density Function (PDF)
#TODO: PDF formula, move PDF etc. to separate files
$$
TODO
$$
Therefore:
$$
Pr[a \leq X \leq b] = TODO
$$
### Uniform Random Variable
#TODO: This
### Expected Value
Discrete:
$$
E[X] = \sum\limits_{i}X_{i}\ Pr[X = X_{i}]
$$
Continuous:
$$
E[X] = \int x\ p(x)\ dx
$$
#### Linearity
#TODO: This
#### Strong Law of Large Numbers
Random samples will converge to the expected value.
### Functions of Random Variables
$$
Y = f(X)
$$
#### Expected Value of Functions
Can use the original random variable:
$$
E[Y] = E[f(X)] = \int f(x)\ p(x) dx
$$
### Variance
#TODO: Slide 36
## Formula
#TODO: This formula
$$
\int_{D} f(x)\ dx = \int_{D} \left[ \frac{f(x)}{p(x)} \right] p(x)\ dx \approx \#TODO
$$
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
* Unbiased Estimator #TODO: Own file for this
	* Expected value equals integral
* Higher dimension extension straight forward
* Convergence: $\mathcal{O}(\frac{1}{\sqrt{N}})$
	* Reduce the error by 2: 4 times as many samples
## Sampling Random Variables
For more complex domains, like spheres, hemispheres, squares, ...
### Example: Uniformly Sampling a Disk
PDF: Uniform probability density on unit disk #TODO
$$
p(x,y) = TODO
$$
Goal: Draw samples distributed as: #TODO 
Problem: Pseudo random number generators give us only canonical uniform distribution.
### Rejection Sampling
```c
do {
	// sample
} while (sample_invalid)
```
#TODO: Code for disk, sphere, hemisphere

Note: could scale z $[0,1]$ too
Note: Flipping the hemisphere vector for performance
#### Properties
Pros:
- Flexible
Cons:
- Inefficient
- Problems with low-discrepancy sampling

Used for: Complex shapes. If you have an analytical solution (See [[CG04V2 Monte Carlo#Inversion Method Process]]), use that.
## Importance Sampling
Assume: $p(x) = cf(x)$ ($f$ our integrand)
#TODO: Slide 75
Optimally: PDF cancels out. However, usually that's not possible to exactly cancel. Even matching the shape roughly is much better!

Common strategy: Sample proportional to the integrand (or on one term of the integrand).
### Sampling Arbitrary Distributions
#### Inversion Method Process
1. Compute the CDF $P(x) = \int^{x}_{0} p(x')\ dx$
	1. Antiderivative of wished for $p(x)$
2. Compute inverse $P^{-1}(x)$
3. Obtain uniform $\xi$
4. Compute $X_{i} = P^{-1}(\xi)$
![[Inversion Method.png]]
#### Transforming Between Distributions
Given: n-dimensional random variable $X_{i} \sim p_{x}(X)$
Goal: Distribution of $Y_{i} = T(X_{i})$

New density is:
$$
p_{y}(y) = p_{y}(T(x)) = \frac{p_{x}(x)}{|J_{T}(x)|}
$$

Idea: Jacobian determinant describes local stretching of $T$.
#TODO: Example of applying this in linear map
### Sampling Examples
#TODO: Linear Map
#TODO: 2D Distribution via marginal density
#### Uniform Sampling of a Disk
Note: Switch from x,y to r,theta: We start with x^2, y^2 in the formula, then we want to switch to polar. #TODO: This
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
## More integration dimensions
* Anti-aliasing (image space)
* Light visibility (surface of area lights)
* Depth-of-field (camera aperture)
* Motion blur (time)
* Many lights
* Multiple bounces of light
* Participating media (volume)
## Low Discrepancy Sampling
e.g. Stratified Sampling