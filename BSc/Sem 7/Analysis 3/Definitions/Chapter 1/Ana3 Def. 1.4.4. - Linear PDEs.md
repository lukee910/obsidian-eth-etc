---
mathLink: Linear PDE
tags:
  - NoteType/Definition
---
## Symbol

Linear PDE ^symbol
## Definition

A PDE is linear, if it's of the form: $a^{(0)}u + \Sigma_{i_1=1}^n a_{i_1}^{(1)} u_{x_{i_1}} + \Sigma_{i_1=1, i_2=1}^n a_{i_1, i_2}^{(2)} u_{x_{i_1}x_{i_2}} + \ldots := \mathcal{L}[u] = f(x)$ ^definition

Where $x = (x_1, \ldots, x_m)$ and $f(x), a_{i_1, \ldots, i_m}^{(m)}$ functions of x.

## Notes

Not linear examples:
- $uu_x = 0$
- $u^2 = 0$
Linear examples:
- $u_{tt} = u_{xxxx}$

Solutions:
If $u$ and $v$ solve the PDE, then $u-v$ solves the PDE with $f = 0$.