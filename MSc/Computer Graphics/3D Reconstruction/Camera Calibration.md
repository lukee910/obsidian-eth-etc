Camera projects 3D world points onto 2D image plane.

Objective is to find:
- Optical center
- Focal length
- Distortion parameters
## From Pattern
Picture of a checkerboard pattern with known dimensions. Plane to make stuff simpler.
## Calculating the parameters
Assuming the calibration paper is on a plane, $z=0$:
$$
\begin{align}
p_{2d} = \begin{pmatrix}
f_{x} & 0 & c_{x} \\ 0 & f_y & c_y \\ 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
r_{11} & r_{12} & r_{13} & t_{1} \\ r_{21} & r_{22} & r_{23} & t_{2} \\ r_{31} & r_{32} & r_{33} & t_{3} \\
\end{pmatrix}
\begin{pmatrix}
x \\ y \\ 0 \\ 1
\end{pmatrix}
\end{align}
$$
This simplifies into (remove $r_{i3}$ and $z$):
$$
\begin{align}
p_{2d} = \begin{pmatrix}
f_{x} & 0 & c_{x} \\ 0 & f_y & c_y \\ 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
r_{11} & r_{12} & t_{1} \\ r_{21} & r_{22} & t_{2} \\ r_{31} & r_{32} & t_{3} \\
\end{pmatrix}
\begin{pmatrix}
x \\ y \\ 1
\end{pmatrix}
\end{align}
$$
This version of $K \cdot E$ build a homography between the top-down view and the actual camera: [[Homography (Computer Vision)]]
## Homography Estimation
#TODO #Later: Slides 19 slide 31-36, homography estimation
