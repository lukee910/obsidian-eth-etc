Note: See Analysis II cheat sheet.
## Derivation/Integration Rules
### Trigonometric Derivations
- $sin' = cos$
- $cos' = -sin$
- $tan' = \frac{1}{cos^{2}}= 1 + tan^{2}$
### Analysis II Cheat Sheet Rules
$$
\begin{array}{ccc}
  f'(x) & f(x) & F(x) \\
  \hline
  a \cdot x^{a-1} & x^a & \frac{x^{a+1}}{a+1} \\
  \frac{a}{x^{a+1}} & \frac{1}{x^a} & \frac{1}{(x^{a-1})(-a + 1)} \\
  \frac{-1}{x^2} & \frac{1}{x} & \ln |x| \\
  \frac{1}{2\sqrt{x}} & \sqrt{x} & \frac{2}{3} x^{\frac{2}{3}} \\
  \hline
  \sin(2x) & \sin^2(x) & \frac{1}{2}\left( x - \frac{1}{2} \sin(2x) \right) \\
  -\sin(2x) & \cos^2(x) & \frac{1}{2}\left( x + \frac{1}{2} \sin(2x) \right) \\
  \frac{1}{\cos^2(x)} = 1 + \tan^2(x) & \tan(x) & -\ln |\cos(x)| \\
  -\frac{1}{\sin^2(x)} & \cot(x) & \ln |\sin(x)| \\
  \frac{1}{\cosh^2(x)} & \tanh(x) & \ln |\cosh(x)| \\
  \frac{1}{\sqrt{1 - x^2}} & \arcsin(x) & x \cdot \arcsin(x) + \sqrt(1 - x^2) \\
  -\frac{1}{\sqrt{1 - x^2}} & \arccos(x) & x \cdot \arccos(x) - \sqrt(1 - x^2) \\
  \frac{1}{1 + x^2} & \arctan(x) & x \cdot \arctan(x) - \frac{1}{2} \ln(1 + x^2) \\
  \frac{1}{\sqrt{x^2 + 1}} & arcsinh(x) & x \cdot arcsinh(x) + \sqrt(x^2 + 1) \\
  \frac{1}{\sqrt{x^2 - 1}} & arccosh(x) & x \cdot arccosh(x) + \sqrt(x^2 - 1) \\
  \hline
  c \cdot e^{cx} & e^x & \frac{1}{c} \cdot e^{cx} \\
  \frac{1}{\ln(a) \cdot x} & \log_a |x| & \frac{x}{\ln(a)} (\ln|x| - 1) \\
  \frac{1}{x + c} & \ln |x + c|
\end{array}
$$
## Integrating over the Hemisphere
With substitution $d \vec{\omega} = \sin(\theta)\ d\theta\ d\phi$:
$$
\int_{H^{2}} f(\vec{\omega})\ d \vec{\omega} = \int_{\theta=0}^{\frac{\pi}{2}} \int_{\phi=0}^{2\pi} g(\theta, \phi) \sin(\theta) \ d\theta\ d \phi
$$
Note the integration bounds.
## Jacobian
![[Jacobian.png]]

