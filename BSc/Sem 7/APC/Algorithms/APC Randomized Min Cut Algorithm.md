---
aliases: []
tags:
  - NoteType/Algorithm
  - CompSci/Theoretical/Algorithmics/Probabilistic
  - CompSci/Theoretical/Algorithmics/Graphs
---
## Problem

[[Minimum Cut Problem]]

## Algorithm

Using [[Basic Random Min Cut Algorithm#^RandomContract|RandomContract]]

$MinCut(G):$
- if $n \leq 16$
	- Compute $\mu(G)$ deterministically
- else
	- $t \leftarrow \lceil \alpha n \rceil + 1$
	- $H_1 \leftarrow \text{RandomContract}(G, t)$
	- $H_2 \leftarrow \text{RandomContract}(G, t)$
	- return $\min(MinCut(H_1), MinCut(H_2))$ // recurse

Note: 16 may be replaced by other values. 16 makes for easy analysis.

## Complexity

Time: $O(n^2 \log n)$
Space:

## Approach Explanation

Improve [[Basic Random Min Cut Algorithm]] with bootstrapping.

Idea: Basic algorithm fails for fewer edges. Use same algorithm, but with better chances, with recursion.

## Proofs

Runtime recursion: $t(n) \leq O(n^2) + 2t(\lceil \alpha n \rceil + 1)$.

[[APC Lemma 1.2]]
[[APC Lemma 1.3]]
[[APC Lemma 1.4]]

[[APC Theorem 1.5]]