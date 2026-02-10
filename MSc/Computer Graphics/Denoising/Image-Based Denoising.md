## Setup
For each pixel, apply filter/kernel of weighted average from neighbourhood.

We want a filter that is:
- Flexible: Arbitrary filter support
- Robust: Few denoising artifacts
## Denoising Approaches
### Bilateral Filter
First approach, was quite good.

Per pixel weight $w(p,q)$ based on generalized distance $d$ of:
- spatial (in pixels) $\rightarrow$ decrease exponentially
- range (difference in value $u$)
$$
d^{2}(p,q) = \frac{(u(p) - u(q))^{2} - 2 \sigma^{2}}{\varepsilon + k^{2} \cdot 2\sigma^{2}}
$$
Where:
- $\sigma$ is the noise variance of the image.
- $k$: #TODO
- $\varepsilon$: Prevent division by 0
Do this per colour channel.

Apply this on a patch of size $2f+1$ pairwise. Increasing $f$ makes it blurrier, but removes noise.
### Non-Local Means Filter (NL-Means)
`Buades et. al 2006`
Development with speed improvement of [[#Bilateral Filter]].
#### NL-Means with Non-Uniform Variance
$$
d^{2}(p,q) = \frac{(u(p) - u(q))^{2} - Var[p] + \min(Var[q], Var[p])}{\varepsilon + k^{2} \cdot (Var[p] + Var[q])}
$$
## Applying Denoising to Monte Carlo Ray Tracing
Problem: Variance is non-uniform, both spatially and per channel. Hence, [[#NL-Means with non-uniform variance]].
## Variance Estimation
#TODO: Sample mean variance vs sample variance
### Sample Mean Variance (Independent Samples)
Use sample mean variance:
$$
Var[p] = \left( \frac{1}{n-1} \sum\limits_{i=1}^{n}(x_{i} - \bar{x})^{2} \right) / n
$$
Where the term in the brackets is the sample variance.
Where:
- $n$ is the number of samples within $p$
- $\bar{x}$ is the average value of all samples within $p$
- $x_{i}$ is the value of a sample within $p$
### 2-Buffer Variance (Correlated Samples)
For any option in [[Sample Placement - Overview#Approaches]], the independent approach does not work.

Idea: Generate two images with different RNG seeds. Compute the variance estimate across these two images (image difference squared divided by four).

Two series of samples ($x_{i,\ldots}$) with $N$ samples each.
$$
Var[p] = \frac{1}{4} \left( \sum\limits_{i=1}^{N} x_{i,1} - \sum\limits_{i=1}^{N} x_{i,2} \right)
$$

Problem: The variance itself is noisy, since it's only based on two samples.

Solution: Blur the variance and take $\max(\text{VarianceMap}, \text{BlurredVarianceMap})$.
## Leveraging Scene Data
Idea: We have the scene geometry etc., use this.

We use the following buffers from the camera perspective:
- Normal
- Texture
- Depth
### Joint NL-Means
Note: This assumes noise free features.

#TODO: Feature distance
$$
d^{2}_{f}(p, q) = \arg \max_{j\in [1..M]} \Phi^{2}_{j}(p, q)
$$
$$
w_{f}(p, q) = \exp(-d^{2}_{f}(p,q))
$$
#TODO: Joint feature things
Note: This is pixel based, NOT patch based!
### Noisy Features
Problem: With few samples, noise in features gets applied to image (style transfer ish).

Trick: Blur filter the noise buffer. The signal to noise ratio is much better, so this works fine.
## Space-Time Filtering
Note: For videos, spatial filtering can create flickering blotches from the noise result.

Space-time filtering adds correlation from frame to frame to reduce how much the change in blotching noise jumps out.
## A Posteriori Methods
Very effective, often used in production.
- Preserve generality of MC rendering
- Low computational overhead
- Moderately intrusive for the renderer

Problems:
- Residual low-frequency noise
- Not robust at low sampling rates
	- Use larger feature and temporal windows, e.g. DLSS 32 frames
- Conflicting constraints (moving FG vs static BG, ...)
- Many parameters to tune
## NFOR
`Bitterli at al 2016`
Last non-neural denoising project.
## Limitations of Image-Based Renderers
- #TODO: First limitation
- Residual noise along edges
