Goal: Find embedding in vector space that carries meaning.

Note: Embed based on (fixed-size) context around it!

## Skip-Gram Model

Input: Sequence of words $x = x_1, \ldots, x_T$
Goal: Learn parameters $\theta$ s.t. each word predicts its context words.

Context window: $I = \{ -R, \ldots, -1, 1, \ldots, R \}$ (words at radius $R$ around center word)
Log-Likelihood:
$$
l(\theta; x) = \sum^{T}_{t=1}\sum_{\Delta \in I} \log p(x_{t+\Delta} | x_t; \theta)
$$
($x_{<0},\ x_{>T}$ use special padding symbol, e.g. \<PAD>)

Model as Bi-linear model:
$$
\begin{align}
	\ln p(v | w) &= <z_w, z_v> + const \\
	\Rightarrow p(v | w) &= \frac{\exp(<z_w, z_v>)}{\sum_u exp(<z_w, z_v>)}
\end{align}
$$
-> If words occur together, their dot product is higher

However:
* Different embeddings for conditioned vs predicted word ($\zeta_w^T$)
* Add a bias

$$
p(v | w) = \frac{\exp(<\zeta_w^T, z_v> + b_v)}{\sum_u exp(<\zeta_w^T, z_v> + b_u)}
$$

### Log-likelihood
$N_vw = |\{ t: x_t = w,\ x_{t+\Delta} = v,\ \Delta \in I \}|$
$$
l(\theta; x) = \sum_{v,w} N_{vw}\left[ \exp(<\zeta_w^T, z_v> + b_v) - \ln \sum_{u \in \Sigma} exp(<\zeta_w^T, z_v> + b_u) \right]
$$

## Binary Classification Model

Prediction task, run a binary classification of word pairs as likely co-occurrences.

For each word pair $(w,v)$: $p(v | w) = \sigma(<\zeta_w, z_v> + b_v)$

### Logistic log-likelihood
$$
l(\theta; x) = \sum_{(w,v) \in S^+} \ln \sigma(v, w; \theta) + \sum_{(w,v) \in S^-} \ln (1 - \sigma(v, w; \theta))
$$
Positive sample set: $S^+ = [(x_t, x_{t+\Delta}): t = 1,\ldots,T,\ \Delta \in I]$
Negative sample set: randomly sample some words. Random words will most likely not co-occurr.
$S^- = [(x_t, x_{tj}): t = 1,\ldots,T,\ v_{tj} \sim_{iid} q,\ j=1,\ldots,r]$
$q$: Noise distribution of words (e.g. word frequency based)
$r$: Number of negative samples we want per word.

### Relation to Skip-Gram
This formalizes the Skip-Gram problem, kind of an implementation?

### Negative Sampling Distribution
General form:
$$
q(w) \propto p(w)^\alpha,\ \alpha \geq 0
$$
$p(w)$: empirical word frequency in corpus
$\alpha$: flattening the distribution. Common choice: $\alpha = \frac{3}{4}$
=> Don't oversample high frequency words, like pronouns

## Global Word Vectors = GloVe

Word embeddings via matrix factorization. UV should approximate $N_{vw}$.
![[GloVe ojective.png]]
![[GloVe weigh fn.png]]

Can use asymmetric loss, e.g. $\ln \hat{p}(v,w) = <\zeta_w, z_v>$

