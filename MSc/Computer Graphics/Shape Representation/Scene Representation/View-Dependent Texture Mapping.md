Campanile, Debecev et al. 1996

Geometry modeling: Assume we have the geometry (i.e. manual model similar to scene), can we map the texture onto it?
## Unstructured Lumigraph
Buehler et al. 2001

Rendering algorithm that takes into account the strategy of [[View-Dependent Texture Mapping]].

Limitations:
- Sensitive
- #TODO: Other constraints
### Blending Fields
Weighted blend of the camera perspectives, based on penalties (e.g. position and angle).
$$
color_{desired} = \sum\limits_{i} w_{i} color_{i}
$$
