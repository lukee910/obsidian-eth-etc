Area light applied on a mesh. Each surface point emits given [[Radiance]] $L_{e}$.
## $L_{e}$
Directly return $L_{e}$.
## Importance Sampling
Notation:
- $A(i)$: Area of face $i$
- $A$: Total area, $A = \sum A(k)$
- $p_{A}(x)$: PDF of choosing any given point
### Preprocess
Build discrete PDF $p_{\Delta}$ for choosing polygons (triangles) proportional to their area:
$$
p_{\Delta}(i) = \frac{A(i)}{A}
$$
### Runtime
1. Sample polygon $i$ ($p_{\Delta}(i)$) and a point $x$ on $i$ (uniformly)
2. Compute PDF of choosing the point $x$ overall:
   $$p_{A}(x) = p_{Delta}(i) p_{A}(x | i) = \frac{1}{A}$$
