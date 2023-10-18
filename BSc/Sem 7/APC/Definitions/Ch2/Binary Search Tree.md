---
mathLink: 
tags:
  - NoteType/Definition
  - ETH/BSC/S7/APC
---
## Symbol

$B_S$ ^symbol
## Definition

$$
B_S =
\begin{cases}
	\lambda & S = \emptyset \\
	\text{Tree with root $x$, left child $B_{S^{<x}}$, right child $B_{S^{>x}}$} & else
\end{cases}
$$^definition

Using:
- $\lambda$ is the empty tree
- $S^{<x} := \{ a \in S\ |\ a < x \}$
- $S^{>x} := \{ a \in S\ |\ a < x \}$
