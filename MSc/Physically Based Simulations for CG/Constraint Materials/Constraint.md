## Definition
A constraint $C(x_{1}, \ldots, x_{n}) : \mathbb{R}^{3n} \to \mathbb{R}$ is:
- A scalar-valued function of one or several arguments
- An implicit expression for a relation that must hold between its arguments
## Satisfied
A constraint is *satisfied* if $C = 0$.
This is a convention.
## Examples of n-ary Constraints
- Constant position: $C(x_{1})$
- Constant distance: $C(x_{1}, x_{2})$
- ...constant area, volume for 3-ary and 4-ary constraints.
## Soft vs Hard
### Soft Constraints
Idea: Introduce forces that pull system towards $C = 0$ configurations.

Set up a [[Penalty Function]] and its [[Penalty Force]] to encourage/enforce it.
### Hard Constraints
