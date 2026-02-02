[[Rendering Equation]] term $L_{i}$: Light is from a reflection on another surface:
$$
L_{i}(x, \vec{\omega}) = \int_{H^{2}} f_{r}\left((r(x, \vec{\omega}), \vec{\omega}_{i}', -\vec{\omega}\right) L_{i}\left( r(x, \vec{\omega}), \vec{\omega}_{i}' \right) \cos \theta_{i}'\ d\vec{\omega}_{i}'
$$
Where:
- Represents the second term of the [[Rendering Equation]] ($L_{r}$) at the next bounce
- $r(x, \vec{\omega})$ is the closest intersection
- $\vec{\omega}$ comes from $d\vec{\omega}_{i}$ in the [[Rendering Equation]] integration
