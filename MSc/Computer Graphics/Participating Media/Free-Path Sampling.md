## Idea
Get the next interaction with the medium. The thinner the [[Participating Media]], the longer the free path.
## Sampling
#TODO: Slides 16 slide 76-77
## Sampling Examples
### Homogeneous Media
$$
T_{r}(t) = e^{-\sigma_{t}(t)}
$$
PDF:
$$
\begin{align}
p(t) &\propto e^{-\sigma_{t}(t)} \\
p(t) &= \frac{e^{-\sigma_{t}(t)}}{\int_{0}^{\infty} e^{-\sigma_{t}(s)}\ ds} = e^{-\sigma_{t}(t)}
\end{align}
$$
#TODO: Slides 16 Slide 78
#### Homogeneous Sampling Recipe
- Generate random number $\xi$
- Compute distance $t = -\frac{\ln(1 - \xi)}{\sigma_{t}}$
- Compute PDF $p(t) = \sigma_{t}e^{-\sigma_{t}(t)}$

What if we hit a surface first at $s < t_{max}$ (with $t_{max}$ the extent of the volume)?
- Generate random number $\xi$
- Compute distance $t = s$
- Compute PDF $p(s) = e^{-\sigma_{t}(s)}$ (= [[Participating Media Radiance#Transmittance|Transmittance]])

Choose approach based on which case we have, where the surface we hit is.
### Heterogeneous Media
$$
T_{r}(t) = e^{\int^{t}_{0} -\sigma_{t}(s)\ ds}
$$
Simple cases have analytical solutions, but in practice, use one of the following approximate solutions:
- Regular tracking (3D DDA)
- Ray marching
- Delta tracking
#### Regular Tracking
Assumption: Piecewise-simple / piecewise-constant extinction $\sigma_{t}$.
#TODO: Formula
Recipe:
- March until $T_{r}(x_{0}, x_{i}) < \xi$
- Use closed-form solution within the last segment to find exact location of $\xi$
![[Free-Path Sampling Regular Tracking.png]]
#### Ray Marching
Same as [[#Regular Tracking]], but with a fixed march length.

Pros:
- Simpler
Cons:
- Biased
	- Need very small steps to prevent bias
- Sensitive to resolution, may miss cells completely

#TODO: Formula
![[Free-Path Sampling Ray Marching.png]]
#### Delta Tracking
Use this if you want unbiased sampling.

[[Delta Tracking]]

Transmittance via delta tracking:
- Sample free path from $x$ towards $y$
- If a real collision occurs before $y$, then $T_{r}(x, y) = 0$. Else $T_{r}(x, y) = 1$.