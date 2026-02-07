Note: Unit Sphere
## Formulas
$$
\begin{align}
\vec{\omega}_{z} &= 2 \xi_{1} - 1 \\
r &= \sqrt{1 - \vec{\omega}_{z}^{2}} \\
\phi &= 2 \pi \xi_{2} \\
\vec{\omega}_{x} &= r \cos \phi \\
\vec{\omega}_{y} &= r \sin \phi
\end{align}
$$
## Derivation
Use [[Archimedes' Hat-Box Theorem]] instead of [[Area-Preserving Sampling]] for the above result.

Idea: Sample the height first and get the corresponding radius on the disk (at $z=0$) for that (via Pythagoras). Then, uniformly sample the angle and convert to $x,y$ Cartesian.

