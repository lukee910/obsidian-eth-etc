## 2.4.2
Separate loss to depend on a column $v_j$ of $V$:
$$
	l_U(v_j) = \frac{1}{2}v_j^T(\Sigma_i \omega_{ij} u_i u_j^T + 2 \lambda I) v_j - (\Sigma_i \omega_{ij} a_{ij} u_i^T) v_j
$$
Consider U as fixed, get improvement:

$$
	v_j^* = (\Sigma_i \omega_{ij} u_i u_j^T + 2 \lambda I)^{-1} \cdot (\Sigma_i \omega_{ij} a_{ij} u_i)
$$
## 2.4.3 Alternating Subspace Optimization

$V^{t+1} \leftarrow \arg \min_{V} l(U^t, V),\ U^{t+1} \leftarrow \arg \min_{U} l(U, V^t)$

Note: Only finds local minimum.