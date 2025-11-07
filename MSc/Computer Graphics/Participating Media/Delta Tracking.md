Unbiased technique for [[Free-Path Sampling]]. Inspired by rejection sampling.

Idea:
- Add a fictitious volume
- Combined volume (real + fictitious) is homogenous
- Generate (tentative) free-paths analytically
- Probabilistically reject/accept collisions based on local concentrations of real vs fictitious volumes.
## Majorant Extinction
Majorant extinction $\bar{\sigma}_{t}$ represents fictitious and real extinction combined.
#TODO: Majorant Extinction
## Notes
- Tight bound of majorant is good, use the max real extinction
- Use a grid/octree/kd-tree to subdivide space and precompute localized (tighter) majorants
