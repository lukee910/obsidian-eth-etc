## MC Integration II & Light Sources
### 1.1 Half-Direction Transform
[[Solid Angle#Differential Solid Angle]]

#Unclear: Why does the law of reflection apply here, how are we oriented around $\vec{\omega}_{i}$?
### 1.2 Area/Hemispherical Transform
Relation between area domain and hemispherical domain.
[[Solid Angle]]

Note: Seemingly, the formula given already is the determinant of the Jacobian.

Solution:
The jacobian determinant relates the differential quantities in different domains. In this case, the differential area patch $dA$ at y [[Subtended Angle (Geometry)|subtends]] a differential solid angle $d \vec{\omega}_{i}$ at $x$. Here, we observe that as the points x and y get farther apart, the area patch subtends a smaller solid angle, which is captured by the inverse relation to the distance. Then, we observe that as the patch faces away from x, it subtends a smaller angle. This diminishes to 0 when the patch direction is orthogonal to $\vec{y} - \vec{x}$. This is captured by the dot product.
### 1.3 MC Integrator
[[_T Monte Carlo Integration]]

![[Monte Carlo Estimator]]

### 1.4 Point Light Power
[[Lambert's Cosine Law]]: In this setup, $dA(x) = \cos\theta\ dx\ dy$

Note: Integration-Wizardry, that's _not_ happening at the exam.
