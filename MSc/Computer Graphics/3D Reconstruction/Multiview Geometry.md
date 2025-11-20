## Epipolar Geometry
![[Epipolar Geometry.png]]
Two cameras (at $O_{1}, O_{2}$) looking at point $P$.
$e, e'$ are the Epipoles, center of one camera on the center of the other camera. All lines from camera 1 will originate at $e'$ when seen from camera 2.

Project line from other camera based on mutual camera positions. Blue lines are the Epipolar Lines.
## Essential Matrix
### Setup
We first assume canonical cameras:
$$
K = K' = I
$$
Then, the projection matrices can be simplified:
- $P=[I, 0]$ ($I$ identity direction, $0$ origin location, can fix one camera here)
- $P'=[R, T]$
### Finding the essential matrix
![[Essential Matrix - Vector Normal to Epipolar Plane.png]]
#TODO: Slide 43-44
### Essential Matrix Definition
#TODO: Slide 44
## Fundamental Matrix
[[#Essential Matrix]], but we take $K$ into account (drop assumption from [[#Essential Matrix]]).

Definition:
$$
\begin{align}
p'^{T} K'^{T}[T_{x}]RK^{-1}p &= 0 \\
\Leftrightarrow p'^{T} F p &= 0
\end{align}
$$
