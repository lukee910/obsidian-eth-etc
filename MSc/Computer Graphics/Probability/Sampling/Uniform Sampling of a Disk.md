Note: Unit Disk
## Formulas
[[Probability Density Function|PDF]]:
$$
\begin{align}
p_{p}(r, \theta) &= p_{p}(r, \theta) = \frac{r}{\pi} \\
p_{c}(x, y) &= \begin{cases}
\frac{1}{\pi} & x^{2} + y^{2} < 1 \\
0 & \text{else}
\end{cases}
\end{align}
$$
Sampling:
$$
\begin{align}
r &= \sqrt{\xi_{1}} \\
\theta &= 2 \pi \xi_{2}
\end{align}
$$
## Derivation
Recipe: [[Area-Preserving Sampling]]
### 1. Desired Probability Density
Convenient coordinate system: Cartesian

$$
p_{c}(x, y) = \begin{cases}
\frac{1}{\pi} & x^{2} + y^{2} < 1 \\
0 & \text{else}
\end{cases}
$$
### 2. Other Coordinates with Easy Parameterization
$r, \theta$ where:
$$
\begin{align}
x &= r \cos \theta \\
y &= r \sin \theta
\end{align}
$$
### 3. Relate PDFs in Two Systems
[[CG 04V2 Monte Carlo#Jacobian Method]] in the [[CG 04V2 Monte Carlo#General Case|General Case]]:

Transformation: $T(r, \theta)$ applies the parameterization above:
$$
T(r, \theta) = \begin{pmatrix}
r \cos \theta \\ r \sin \theta
\end{pmatrix}
$$

PDF:
$$
p_{c}(x, y) = p_{c}(T(r, \theta)) = \frac{p_{p}(r, \theta)}{|J_{T}(r, \theta)|}
$$

[[Jacobian]]:
$$
J_{T}(r, \theta) = 
\begin{bmatrix}
\cos \theta & -r \sin \theta \\ \sin \theta & r \cos \theta
\end{bmatrix}
$$
Jacobian determinant:
$$
|J_{T}| = r(\cos^{2}\theta + sin^{2}\theta) = r
$$
We get:
$$
\begin{align}
p_{c}(x, y) &= \frac{p_{p}(r, \theta)}{|J_{T}(r, \theta)|} \\
\Leftrightarrow p_{p}(r, \theta) &= |J_{T}(r, \theta)| p_{c}(x, y) \\
&= r p_{c}(x, y) \quad \text{Insert } |J_{T}| \\
&= \frac{r}{\pi} \quad \text{Insert definition of } p_{c}
\end{align}
$$
### 4. Compute Marginal, Conditional PDFs
[[Marginal Density]]:
$$
p(r) = \int_{0}^{2\pi} p_{p}(r, \theta)\ d \theta = \int_{0}^{2\pi} \frac{r}{\pi}\ d\theta = 2r
$$
[[Conditional Density]]:
$$
p(\theta|r) = \frac{p_{p}(r, \theta)}{p(r)} = \frac{\frac{r}{\pi}}{2r} = \frac{1}{2\pi}
$$
### 5. Sample 1D PDFs Using Inversion Method
[[CG 04V2 Monte Carlo#Inversion Method Process]]
1.: [[Cumulative Distribution Function|CDF]]
$$
\begin{align}
P(r) &= \int_{0}^{r} p(r')\ dr' \\
&= \int_{0}^{r} 2r'\ dr' = [r'^{2}]_{0}^{r} \\ &= r^{2}
\end{align}
$$
$$
P(\theta|r) = \int_{0}^{\theta} \frac{1}{2\pi}\ d\theta = \frac{\theta}{2\pi}
$$
2-4.: Inverting, get $\xi = P^{-1}$:
$$
\begin{align}
\xi_{1} = r^{2} &\Rightarrow r = \sqrt{\xi_{1}} \\
\xi_{2} = \frac{\theta}{2\pi} \xi_{1} = r^{2} &\Rightarrow \theta = 2 \pi \xi_{2}
\end{align}
$$







