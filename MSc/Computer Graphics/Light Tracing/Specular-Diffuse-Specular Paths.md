## Problem
LSDSE paths have trouble meeting in the diffuse in the middle. E.g. pool caustics.
## Idea
Just pretend the paths met anyways.

Approaches:
- Make specular BRDFs *slightly* glossy, add a bit of blur. Gets rid of many issues in production rendering.
- [[Photon Mapping]]
