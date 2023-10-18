---
aliases:
  - BasicMinCut
tags:
  - NoteType/Algorithm
  - CompSci/Theoretical/Algorithmics/Graphs
  - CompSci/Theoretical/Algorithmics/Probabilistic
---
## Problem

[[Minimum Cut Problem]]

## Algorithm

RandomContract ^RandomContract
- while $|V| > 2$
	- pick $e \in E$ u.a.r., add $e$ to cut
	- $G \leftarrow G/e$
- return size of only cut in $G$

Run this $N$ times and return the smallest MinCut found.

## Complexity

Time:
- Expected: $O(n^4)$
	- $O(n^2)$ for RandomContract
	- $O(n^2)$ for $N = cn(n-1)$ for some $c$
Space:

## Approach Explanation

Maintain a multigraph that allows:
- Edge contraction in $O(n)$
- Choose edge u.a.r. in $O(n)$
- Find number of edges between two given vertices in $O(1)$ ($O(n)$ would suffice)

$N$: For $N = 10n(n-1)$, $\mathbb{P}[\text{N failures}] \leq e^{-20} < 10^{-8}$.

## Proofs

### Observation 1.1 #ETH/BSC/S7/APC 
Let $G$ be a multigraph and $e \in E$. Then $\mu($[[Graph G without edge e]]$) \geq \mu(G)$. Moreover, if $\exists$ [[Minimum Cut|MinCut]] $C$ in $G$ s.t. $e \notin C$, then $\mu(G/e) = \mu(G)$.

### Lemma 1.2 #ETH/BSC/S7/APC 
Let $G$ be a multigraph with $n$ vertices. Then the probability of $\mu(G) = \mu(G/e)$ for any $e \in E$ u.a.r. is at least $1 - \frac{2}{n}$.

The success probability of the RandomContract is $p_0(n) \geq \frac{2}{n(n-1)}$. $\mathbb{P}[\text{N failures}] = \left( 1 - \frac{2}{n(n-1)} \right)^N \leq e^{-2N/n(n-1)}$. Choose $N$ s.t. this probability is sufficiently small.


