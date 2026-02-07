Idea: Do a bit of rejection sampling in order to get a sample with a higher probability.
## Procedure
1. Sample $N$ random candidates in the domain
2. Evaluate function for all samples
3. Pick with probabilities proportional to the function value
## RIS for PDFs
Goal: Sample proportional to [[Probability Density Function|PDF]] $\hat{p}$
1. Sample candidates $x_{1}, \ldots, x_{N}$
	1. From a source [[Probability Density Function|PDF]] $p$
2. Compute resampling weights
	1. $w_{i} = \frac{1}{N}\frac{\hat{p}(x_{i})}{p(x_{i})}$
3. Choose $x_{s}$ randomly proportional to $w_{i}$
4. Compute unbiased contribution weight
	1. $W_{x_{s}} = \frac{1}{\hat{p}(x_{s})}\sum_{i}^{M} w_{i}$

