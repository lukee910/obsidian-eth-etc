## Setup / Task Handout
Setup: Contact Simulation (Sphere Collider vs Spring Network). Find static equilibrium.

Note: Our setup doesn't enforce contact, only encourage it. Could use something with an asymptote at 0 energy $(r-\varepsilon)^{2}/r^{2}$. Problem is, solver will have trouble finding a solution (slow and accurate vs fast and have some surface penetration).

Simulation in Ex5 in PBS code repo. Fill in `CASDemoApp::computeStretchEnergy()` etc.

Note: In maple, it's easier to calculate vectors rather than matrices, so matrices are stacked into a vector (e.g. `computeStretchHessian` 6x6 matrix)

Note: `Computeistance` is already maple code (they forgot to take it out).

Maple:
- Can use it to solve simple ODEs as well as write code
- Documentation is not good
	- Just ask them, they can give hints or help with getting the solution to work
SymPy:
- SymPy gets worse as code gets more complicated
- They're more equipped for Maple support, know that better
Autodiff:
- If stuff is too complicated, can use that
## Maple
Start new document

Maple has libraries (use: `with(LinearAlgebra):`). Some:
- `LinearAlgebra`
- `VectorCalculus`
- `CodeGeneration`

Assignment: `plv := Vector([...])`

Note:
- Names in maple will use the C++ variables, use the same ones.
- Norm: `Transpose()` from Linear algebra
- Avoid duplication: Type `.` (e.g. after norm)
- Preview can get very complex. Hide it by ending the line with `:`
- Generate degrees of freedom
	- Copy-paste is the usual go to
	- Can also use `op()` from a generated list of symbols
	- Define the list as a variable, then use that variable
- See dimensions via Variables window on the left
- `C()`: Generate code
	- No parameters generates full expression
	- `optimize` parameter: Break up, reuse expressions
	- `resultname`: Well, that one's obvious
	- Copy the code from the preview (line without `:` shows it)
	- Type is not automatically assigned
		- Do that manually
		- Write a script
- Can use the same script, just call `C()` on different variables
- Matrices
	- `C()` generates a two dimensional array output
	- Either update the syntax to Eigen or make it a vector:
		- `convert(d2U, Vector)` (will convert anything into a vector)
- Output is not vectorized. Use an autodiff(?) system to vectorize your code
- Sometimes maple doesn't know the types, will cast
	- `C(.., deducetypes=false)`
	- This shows up in `computeContactHessian` on `(double) E`
- Can reuse the structure of finding the Hessian for our project. Also the variable isolation thing (make it a subfunction to keep the namespace clean)

NOTE: This code doesn't quite work, bricked in the demo. Solution 

```Maple
with(LinearAlgebra):
with(VectorCalculus):
with(CodeGeneration):

p1v := Vector([p1[1], p1[2], p1[3]])
p2v := Vector([p2[1], p2[2], p2[3]])
q1v := Vector([q1[1], q1[2], q1[3]])
q2v := Vector([q2[1], q2[2], q2[3]])

Lp := p2v - p1v
Lq := p2v - q1v
dLp := sqrt(Transpose(Lp) * Lp) // here, use . to get Lp twice (not duplicated)
dLq := sqrt(Transpose(Lq) .)

U := 1/2 * E * (dLq - dLp)^2 :
dU := Gradient(U, [q1[1], q1[2], q1[3], q2[1], q2[2], q2[3]]) // []: which degree of freedom to calc gradient on
d2U := Hessian(U, [q1[1], q1[2], q1[3], q2[1], q2[2], q2[3]])

C(U, optimize, resultname='energy')
C(dU, optimize, resultname='gradient')
C(convert(d2U, Vector), optimize, resultname='hessian')
```

```Maple
// should not be squared, but should also work
dist := (q[1] - pos[1])^2 + (q[2] - pos[2])^2 + (q[3] - pos[3])^2 - r^2
U := 1/2 * E * (dist)^2
dU := Gradient(U, [q[1], q[2], q[3]]):
d2U := Hessian(U, [q[1], q[2], q[3]]):

C(U, optimize, resultname='energy')
C(dU, optimize, resultname='gradient')
C(convert(d2U, Vector), optimize, resultname='hessian')
```

## SymPy
Define symbols, see solution python file.

Code generation:
1. Find common subexpressions
2. Generate code for each expression manually

Note:
- This is not a drop-in replacement because of variable names (e.g. `pos0` instead of `pos[0]`).
- Optimization not easy, but for our level it's fine.

