## Idea
Avoid artefacts of [[Linear Modal Analysis]] by evaluating true nonlinear forces on deformed geometry $f(Uq)$.
## Generalized Non-Linear Forces
Equations of motion: #TODO slide 14

Solve it with Newton's method requires linearization: #TODO:

Big Problem: This creates a dependency on the full-space model.
## Special Case: Cubic Forces
### St. Venant-Kirchhoff and Green Twist
Idea: St. Venant-Kirchhoff energy density
#TODO: Slides 10 Slide 15

Complexity of force is in $\mathcal{O}(r^{3})$ and Jacobian $\mathcal{O}(r^{4})$, independent of full-space size. Generally, $\mathcal{O}(r^{3})$ << $\mathcal{O}(\text{subspace})$.
### Cubature
Idea: Avoid complexity by evaluating force and Jacobian only for a subset of elements. Approximate integral using sparse set of elements.

#TODO: Math of this, slide 17/18.

Note: Get the weights by optimizing on full model in a least-squares sense. For ultra-large models, that preprocessing can take very long (stochastic approaches exist).

Somewhat similar to [[_T Monte Carlo Integration]].

Pros:
- Scale better than [[#St. Venant-Kirchhoff and Green Twist]]
- Faster than cubic polynomials ([Barbic et al 2005](https://graphics.cs.cmu.edu/projects/stvk/))
Cons:
- Cubature incurs errors
- Only pays off for bases with $r \geq 25$
