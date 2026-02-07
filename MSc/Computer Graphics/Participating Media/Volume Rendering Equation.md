$$
\begin{align}
L(x, \vec{\omega}) &= T_{r}(x, x_{z}) L(x_{z}, \vec{\omega}) \\
&+ \int^{z}_{0} T_{r}(x, x_{t}) \sigma_{a}(x_{t})L_{e}(x_{t}, \vec{\omega})\ dt \\
&+ \int^{z}_{0} T_{r}(x, x_{t}) \sigma_{s}(x_{t})L_{s}(x_{t}, \vec{\omega})\ dt
\end{align}
$$
Add all three sources of radiance:
- Reflected from last surface
- [[Participating Media Radiance#Emission]]
- [[Participating Media Radiance#In-Scattering]]
With:
- [[Transmittance]]
	- Including [[Extinction Coefficient]]
- [[Absorption Coefficient]]
- [[Scattering Coefficient]]

Note: $L_{s}$ is also an integral. Expanding yields the final formulation:
$$
\begin{align}
L(x, \vec{\omega}) &= T_{r}(x, x_{z}) L(x_{z}, \vec{\omega}) \\
&+ \int^{z}_{0} T_{r}(x, x_{t}) \sigma_{a}(x_{t})L_{e}(x_{t}, \vec{\omega})\ dt \\
&+ \int^{z}_{0} T_{r}(x, x_{t}) \sigma_{s}(x_{t}) \left( \int_{S^{2}} f_{p}(x_{t}, \vec{\omega}', \vec{\omega}) L_{i}(x_{t}, \vec{\omega}')\ d\vec{\omega}' \right) \ dt
\end{align}
$$
Where the inner integral accounts for the incident light.