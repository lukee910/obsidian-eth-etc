Idea: Shrink the density estimation kernel over the render.

Trick: Do renders at different (very carefully chosen) radius sizes, average them.
## Choosing the Radius
Given:
- $i$: iteration
- $r_{i}$: kernel radius
- $\alpha \in (0,1)$: parameter controlling the shrinking
Radius for next iteration is:
$$
r^{2}_{i+1} = \frac{i + \alpha}{i + 1}r_{i}^{2}
$$
Idea: Bias vs Noise has this pattern:
![[Photon Mapping Bias vs Noise.png]]
### Choosing $\alpha$
Convergence in $\alpha \in (0,1)$, but $\alpha = 2/3$ minimizes the MSE.
## Algorithm
1. Trace Photons
	1. Emit, scatter, store photons
2. Render
	1. Trace camera paths
3. Display running average
4. Compute new radius $r^{2}_{i+1}$ and repeat

Note: Trivial to parallelize by iteration number.
## Notes
Note: No need to bother with caustic photon map, since it'll eventually be sharp anyways.

Note: While Path Tracing handles most of the cases in production, when it can't, they often use [[Progressive Photon Mapping]].
