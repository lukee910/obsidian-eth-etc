## Part 1: Direct Illumination
### 1.1
[[Rendering Equation]]
### 1.2 Ring Light
#### 1) `sampleRing`
Note: You _can_ use [[Rejection Sampling]].
Also see [[Uniform Sampling of a Disk]].

Note: Pay attention to the desired return format.
#### 2) `pdfRing`
$\frac{1}{Area}$
#### 3) `integrateDirect`
[[Reflection Equation]], specifically [[Reflection Equation#Surface Area Integration]] form:
$$
L_{r}(x, z) = \int_{A} f_{r}(x, y, z) L_{i}(x, y) G(x, y)\ dA(y)
$$
With: $z$ unspecified, $x = B$, $y = A$.
## Part 2: Global Illumination and Light Paths
### 2.1
[[Heckbert's Classification]]
[[Next Event Estimation]]
## Part 3: Photon Mapping
### 3.1
[[Heckbert's Classification]]
a) $L(D|S)*D$
b) $$