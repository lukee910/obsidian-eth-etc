# Topic Models
Special case of latent variable models
Latent structure in text data. Used before LLMs. What is this text about?

Documents $i = 1\ldots n$
Document lengths $s_i$
Word positions $t=1\ldots s_i$
Document collection: $X_{it}$ random variables
Realizations $x_{it} \in \Sigma,\ |\Sigma| = m$. $\Sigma$ is vocabulary.
Topics: $k$ topics, $Z_{it} \in \{ 1,\ldots,k \}$

Process: First generate topics, then label the topics.

Assumption: Word order doesn't matter!

Word occurrence of word $w_j$ in document $d_i$:
$$
	N_{ij} = |\{x_{it} = w_j | t = 1,\ldots,s_i\}|
$$
Occurrence matrix: $N = (N_{ij}) \in \mathbb{Z}^{n \times m}_{\geq 0}$. Huge and sparse.

N is minimal sufficient statistics for param estimation.

Complete Data Model:
$$
	(X_{it}, Z_{it}),\ X_{it} \in \Sigma,\ Z_{it} \in \{ 1,\ldots,k \}
$$
![[Topic Models 2 stage sampling.png]]

Characterised by two distributions: Prob of topic given doc, prob of word given topic.

Log-likelihood:
$$
l(\theta; N) = \ln p(N; \theta) = \sum_{i,j} N_{ij} \ln p(w_j | d_i)
$$
Where
$$
	p(w_j | d_i) = \sum^{z=1}_{k} p(w_j | z) p(z | d_i)
$$
(via $p(x_ij | d_i) = p(w_j | d_i) \cdot I_{x_{ij} = w_j}$, which then sums to $N_{ij}$)

This is the **probabilistic Latent Semantic Analysis (pLSA)**.

# Preparatory Session

$k$-dimensional probability simplex: $\Delta^{k-1}$ is the set of $k$-dimensional probability distributions: $x \in [0,1]^k$: $x \in \Delta^{k-1} \Leftrightarrow x_i \geq 0, \sum^{1}_{i=1}x_i = 1$.

## Dirichlet distribution

Distribution over distributions. 

$$
p(v|a) \propto \prod^{k}_{z=1} v_z^{a_z - 1},\quad \alpha_z > 0
$$
## Conjugate priors

Let $p(X | \theta)$ likelihood function, $p(\theta)$ prior. We can compute the posterior by Bayes' rule:
$p(\theta | X) = \frac{p(\theta) p(X | \theta)}{p(X)}$.
If the posterior $p(\theta|X)$ and prior $p(\theta)$ are of the same distribution family, then $p(\theta)$ is the conjugate prior of $p(X | \theta)$.

## Dirichlet & Categorical

Dirichlet distribution is the conjugate for the categorical distribution. (x one-hot encoded)

Prior: $p(\pi) = Dir(\pi; \alpha) \propto \prod^{k}_{j=1} \pi_j^{\alpha_j - 1}$
Likelihood: $p(x_i | \pi) = \prod^{k}_{j=1} \pi^{x_{ij}}$.
Bayes': $p(\pi | X) \propto p(\pi) p (X|\pi)$ etc. 

See: [[Exponent as a sum]]
Which is then $\propto Dir(\pi; \alpha + m)$.
## Logistic Regression

Train on $(X, y)$, where $X \in \mathbb{R}^n,\ y \in \{ 0, 1 \}$.

Sigmoid function:
$$
\sigma(X) = \frac{1}{1 + \exp(-x)}
$$

Prediction: $\hat{y}(x) = \sigma(f(x))$.

## Naive Bayes
Assume features in $x$ are independent, given output class $y$.
$$ p(x_i | y, X_{-i}) = p(x_i | y) $$
Probability given all other $x_{j \neq i}$ is the same as if no other $x_{j}$ were given.
Where $x_{-i} = [x_1,\ldots,x_{i-1},x_{i+1},\ldots,x_d]$.

We classify as follows:
$$
\hat{y}(x) = \arg\max_{y \in Y} p(y) \prod^{d}_{i=1} p(x_i | y)
$$

## Mutual Information

$$
I(X;Y) = H(X) - H(X|Y)
$$
$H(X)$ and $H(X|Y)$ are entropy of $X$ before and after observing $Y$.

Can also be defined as:
$$
I(X;Y) = D_KL(P_{XY} || P_X \cdot P_Y)
$$
I.e. Divergence between marginal distribution of the two vs if we assume that they are independent.

$I(X;Y) = I(Y;X),\ I(X;Y) \geq 0$.

# Topic Models - Lecture 8

## Topic Models ELBO
$$
l(\theta) \geq \sum_{i=1}^{n}\sum_{t=1}^{s_i}\sum_{z=1}^{k} q_{itz} \left[ \ln p(x_{it} | z) + \ln p(z | d_i) - \ln q_{itz} \right]
$$
![[Topic EM Algo.png]]

## Latent Dirichlet Allocation LDA
New documents need a full retraining. How to extend this for new docs?

Notation:
$$
\begin{gathered}
	u_{jz} := p(w_j | z),\ v_{zi} := p(z | d_i) \\
	v \in [0, 1]^k,\ \sum_{z} v_z = 1
\end{gathered}
$$
Define distribution over $v$ mixture vectors.

Use conjugate prior -> compatible with likelihood. For categorical, it's Dirichlet:
$$
p(v|a) \propto \prod^{k}_{z=1} v_z^{a_z - 1},\quad \alpha_z > 0
$$
Typically, fix $\alpha_z = \alpha$ (e.g. $\alpha = 1/k$) and/or optimize $\alpha$ on holdout. Fixed equal $\alpha$ assumes equal topic distribution.

![[LDA Model.png]]

Integrate over all $v_i$ (topic probability given document), parametrized by $\alpha$.
1. Sample distribution from Dirichlet prior ($p(v|\alpha$))
2. Multiply by probability of observing word $x_t$ with these parameters ($p(x_t | U, v)$)
3. Do this for all words $\prod^{t=1}_{s}$
=> Full likelihood of the document $X$, given $U$ (probability of word per topic) and $\alpha$.

LDA can be applied over any document now.

# Probabilistic Matrix Decomposition

Recall: $u_{jz} := p(w_j | z),\ v_{zi} := p(z | d_i)$.

Predicted word frequencies: $p(w_j | d_i) := \hat{N_{ij}}$ as:
$$
\hat{N} = UV,\quad rank(\hat{N}) \leq k
$$
$N_{ij} \approx s_i \hat{N_{ij}}$, where $s_i$ total number of words in document $i$. Not a direct factorization of $N$, but an approximation of relative frequency.

Maximum likelihood objective:
$$
l(U, V; N) = \sum_{i,j} N_{ij} \ln \hat{N_{ij}},\ \hat{N} = UV
$$
Which makes sense since $u,v$ non-negative and sum to one. So, $u,v$ are most effective when $N_{ij}$ is large -> $\hat{N_{ij}}$ should be large if $N_{ij}$ is.

## Non-negative matrix factorization (NMF)

Generally, fully observed:
$$
l(U,V) = \frac{1}{2}||A - UV||^2_F,\ U,V \geq 0
$$
Solution will be sparse, because **cancellations with negative numbers are impossible**! => Often decompositions are (additive) parts, interpretable.

### [[ALS]] for NMF:

After each update, project for constraint:
$$
u_{jz} \leftarrow \max(0, u_{jz}),\quad u_{zi} \leftarrow \max(0, v_{zi})
$$
Possible initialization: non-negative SVD.

## Topic models NMF

Use KL divergence instead of [[Frobenius Norm]]. Use multiplicative updates or ALS.
