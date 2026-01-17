---
aliases:
  - BTDF
  - BSDF
---
BRDF: Bidirectional Reflectance Distribution Function
BTDF: Bidirectional Transmittance Distribution Function

BSDF: Bidirectional Scattering Distribution Function (general term)

$$
f_{r}(x, \omega_{i}, \omega_{r}) = \frac{d L_{r}(x, \omega_{r})}{d E_{i}(x, \omega_{i})} = \frac{d L_{r}(x, \omega_{r})}{L_{i}(x, \omega_{i}) \cos(\theta_{i})\ d \omega_{i}} \quad \left[ \frac{1}{sr} \right]
$$

![[BRDF variables graph.png]]
## Physically-based BRDFs
Needs two properties:
### Helmholtz reciprocity
$$
f_{r}(x, \omega_{i}, \omega_{r}) = f_{r}(x, \omega_{r}, \omega_{i})
$$
### Energy conservation
$$
\int_{H^{2}} f_{r}(\omega_{i}, \omega_{r}) \cos(\theta_{i})\ d\omega_{i} \leq 1,\quad \forall \omega_{r}
$$
## Isotropic
[[Isotropic]] BRDFs scatter the light uniformly. Example: Perfect diffuse.


