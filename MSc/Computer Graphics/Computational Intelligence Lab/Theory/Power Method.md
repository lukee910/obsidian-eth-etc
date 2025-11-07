Computes the principal eigenvector. $A \in \mathbb{R}^{n},\ v \in \mathbb{R}^n$.

1. Initialize a random $v^{(0)} \sim \mathcal{N}(0,I_n)$
2. $v^{(t+1)}=\frac{Av^{(t)}}{\| Av^{(t)} \|}$

Runtime: $\mathcal{O}(Tn^2)$ for $T$ iterations.

[[Remember for Exam]]