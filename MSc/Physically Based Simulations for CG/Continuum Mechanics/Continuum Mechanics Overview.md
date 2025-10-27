## Idea
Start at continuous model, take strain, stress, energy and equilibrium conditions.

Then, discretize with Finite Elements:
* Decompose model into elements (e.g. tetrahedra)
* Formulate discrete energy (and derivates) per element
* Minimize sum of per-element energies
## Pros & Cons
Advantages:
* Accurate material behaviour
* Convergence under refinement
## How to get to our equations
![[CM FEM approaches.png]]
[[Proper FEM Discretization]], [[Discrete Energy Approach]]. We will be using the [[Discrete Energy Approach]].
