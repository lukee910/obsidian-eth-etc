Unbiased technique for [[Free-Path Sampling]]. Inspired by rejection sampling.

Idea:
- Add a fictitious volume
- Combined volume (real + fictitious) is *homogeneous*
- Generate (tentative) free-paths analytically
	- $t = -\frac{\ln(1 - \xi)}{\sigma_{t}}$
	- [[Free-Path Sampling#Homogeneous Sampling Recipe]]
- Probabilistically reject/accept collisions based on local concentrations of real vs fictitious volumes.
## Majorant Extinction
Majorant extinction $\bar{\sigma}_{t}$ represents fictitious and real extinction combined. 
![[Majorant Extinction.png|400]]
At each tentative collision, determine if it's a real collision with the following probability of a real collision $P_{r}$:
$$
P_{r} = \frac{\sigma_{t}(x)}{\bar{\sigma}_{t}}
$$
(Probability of a fake collision $P_{f} = 1 - P_{r}$)
## Notes
- Optimally choose $\bar{\sigma_{t}}$ as the majorant of $\sigma_{t}$, $\bar{\sigma_{t}} = \max_{x} \sigma_{t}(x)$, tight bound preferable.
- Use a grid/octree/kd-tree to subdivide space and precompute localized (tighter) majorants
