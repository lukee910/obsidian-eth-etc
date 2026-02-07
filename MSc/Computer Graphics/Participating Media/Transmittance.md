## Beer-Lambert Law
$$
T_{r}(x, y) = \frac{L_{z}}{L_{0}} = e^{-\sigma_{t}z}
$$
- [[Extinction Coefficient|Extinction Coefficient ($\sigma_t$)]]
- $L_{z}$: Radiance at distance $z$
- $L_{0}$: Radiance at beginning of the beam
![[Beer-Lambert-Law Illustration.png|300]]
#TODO: Derivation on slides 15 slide 31
## Transmittance Homogeneous Volume
$$
T_{r}(x, y) = e^{-\sigma_{t}\|x-y\|}
$$
## Transmittance in Heterogeneous Volumes
$$
T_{r}(x, y) = e^{-\int_{0}^{\|x-y\|} \sigma_{t}(t)\ dt}
$$
## Transmittance Multiplicativity
$T_{r}(x,z) = T_{r}(x,y) T_{r}(y,z)$
For $x,y,z$ in this order along a beam.
