Discrete Shells. Grinspun, Hirani, Schroeder, SCA 2003
## Energy
### Bending Energy
#TODO: Slides 08 Slide 8
### Total Energy
## Simulating It
Simulation requires energy derivatives, which we need angles for.

But: Inverse trigonometric functions are numerically quite unstable, errors explode!
#TODO: Solution via atan(sin / (1 + cos)), why does that work?

Note: Quadratic Discrete Shells and other methods exist