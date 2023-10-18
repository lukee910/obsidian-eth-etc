---
tags:
  - ETH/BSC/S7/APC
---
## Algorithms

### Trick 1

Make some computation in between recursion steps to reduce the problem size. Reduce that aspect of the problem that has the biggest influence on runtime.

Example: Boruvka's Algorithm in [[Randomized MST Algorithm]], random contraction in [[APC Randomized Min Cut Algorithm]].

### Trick 2

Algorithm takes long on the whole problem, however can run fast some part (e.g. for the first few steps or very small subset).

Example: [[APC Randomized Min Cut Algorithm]] for large $m$.

### Trick 4

While recursing, to decrease the chance of failure, duplicate the problem and recurse twice.

Example: [[APC Randomized Min Cut Algorithm]]: $H_1,\ H_2$.

## Maths etc.

### Trick 3

When considering a formula with an arbitrary value, see if you can get rid of some terms by choosing a value containing that term.

Example: [[APC Randomized Min Cut Algorithm]]: Choose $t = n^{2/f(i)}$ s.t. $O(\frac{n^2}{t^2}(n^2 + t^{f(i)}))_{|t=n^{2/f(i)}} = O(n^{4 - 4/f(i)})$, with the sum combining.

