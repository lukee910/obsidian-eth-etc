## Idea
Camera as a projection matrix:
$$
\begin{pmatrix}
p_{11} & \dots&  p_{14} \\ \vdots &  & \vdots \\ p_{31} & \dots & p_{34}
\end{pmatrix}
\begin{pmatrix}
x \\ y \\ z \\ 1
\end{pmatrix}
=
\begin{pmatrix}
u \\ v \\ 1
\end{pmatrix}
$$
Where $\begin{pmatrix}x & y & z\end{pmatrix}^T$ is $P_{3d}$ in world space, $\begin{pmatrix}u & v\end{pmatrix}^T$ is $P_{2d}$ in image space.
## Decomposition
Decompose in intrinsic parameters $K$ and extrinsic parameters $E$.

$$
\begin{align}
\begin{pmatrix}
p_{ij}
\end{pmatrix}_{\substack{i=1..3\\ j=1..4}}
&= K \cdot E \\
&=\begin{pmatrix}
f_{x} & 0 & c_{x} \\ 0 & f_y & c_y \\ 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
r_{11} & r_{12} & r_{13} & t_{1} \\ r_{21} & r_{22} & r_{23} & t_{2} \\ r_{31} & r_{32} & r_{33} & t_{3} \\
\end{pmatrix}
\end{align}
$$

Intrinsic Parameters $K$: Camera properties
- $c_{x}, c_{y}$ scale
- $f_{x},f_{y}$ focal length
Extrinsic Parameters $E$: Position
- $r_{ij}$ Rotation
- $t_{i}$ Translation
## Radial Distortion
Take distortion into account. Be that an artistic effect or a lens correction.

Barrel vs pincushion distortion:
![[Radial Distortion Types.png]]

Brown-Conrady model:
$$
\begin{align}
x_{distorted} &= x(1 + k_{1} r^{2} + k_{2} r^{4} + k_{3} r^{6}) \\
y_{distorted} &= y(1 + k_{1} r^{2} + k_{2} r^{4} + k_{3} r^{6}) \\
\end{align}
$$
Where:
- $r$ is Euclidean distance to the distortion center
- $k_{i}$ are the radial distortion coefficients
	- $k_{1}$ typically determines barrel vs pincushion distortion
	- Depend on camera lens
- Can be extended to also handle tangential distortion (decentering distortion)

