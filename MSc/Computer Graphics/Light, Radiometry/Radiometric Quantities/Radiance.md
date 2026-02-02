$$
L(x, \vec{\omega}) = \frac{d I(\vec{\omega})}{dA^{\perp}(x, \vec{\omega})} \quad \left[ \frac{W}{m^{2}sr} \right]
$$
[[Radiant Intensity]] per perpendicular unit area.
## Relation to Flux
[[Flux]] density per unit [[solid angle]], per perpendicular unit area.

By applying [[Radiant Intensity#Relation to Flux]] to the [[Radiant Intensity]] formulation above we get:
$$
\begin{align}
L(x, \omega) &= \frac{d^{2} \Phi(A)}{d \vec{\omega}\ dA^{\perp}(x, \vec{\omega})}
\end{align}
$$

![[Radiance Flux Shift.png|250]]
By shifting perspective (see image above), this is equivalent to:
$$
\begin{align}
\ldots &= \frac{d^{2} \Phi(A)}{d \vec{\omega}\ dA(x) \cos \theta}
\end{align}
$$
Related to this step: [[Lambert's Cosine Law]].
## Relation to Irradiance
Expressing [[Irradiance]] $E(x) = \frac{d\Phi(A)}{dA(x)} \quad \left[ \frac{W}{m^{2}} \right]$ in terms of [[Radiance]] $L(x, \vec{\omega})$:
$$
\begin{align}
L(x, \vec{\omega}) &= \frac{d^{2}\Phi(A)}{\cos \theta\ dA(x)\ d\vec{\omega}} \\
&= \frac{d(E(x))}{\cos \theta\ d \vec{\omega}} &\Leftrightarrow \\
L(x, \vec{\omega}) \cos \theta\ d \vec{\omega} &= dE(x) &\Leftrightarrow \\
\int_{H^{2}} L(x, \vec{\omega}) \cos \theta\ d \vec{\omega} &= E(x)
\end{align}
$$
"Integrate radiance over hemisphere"
## Relation to Flux
Expressing [[Flux]] $\Phi(A)$ in terms of [[Radiance]].

Start at result from [[#Relation to Irradiance]] $(a)$, insert $E(x) = \frac{d\Phi(A)}{dA(x)} \quad \left[ \frac{W}{m^{2}} \right]$ $(b)$, insert [[#Relation to Irradiance]] again $(c)$:
$$
\begin{align}
\int_{H^{2}} L(x, \vec{\omega}) \cos \theta\ d \vec{\omega} &= E(x) & (a) \\
\int_{A} E(x)\ dA(x) &= \Phi(A) & (b) \\
\int_{A} \int_{H^{2}} L(x, \vec{\omega}) \cos \theta\ d \vec{\omega}\ dA(x) &= \Phi(A) & (c)
\end{align}
$$
"Integrate [[Radiance]] over hemisphere and area"
## Ray Tracing
[[_T Light Tracing]]
- This is the fundamental quantity for ray tracing.
- Remains constant along a ray (in vacuum)
- Incident [[Radiance]] at one point can be expressed as outgoing [[Radiance]] at another point
![[Incident vs outgoing radiance.png]]
