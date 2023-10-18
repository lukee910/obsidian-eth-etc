#ETH/BSC/S7/APC/Ch1
#CompSci/Theoretical/Algorithmics 

## 1.0 Preamble

For recursion $t(n) \leq \alpha n + \beta t(n/2)$: [[Algorithm Runtime]] through $\Sigma_{i=0}^{\log_2 n} (\frac{\beta}{2})^i$
* If $\beta < 2$: $t(n) = O(n)$
* If $\beta = 2$: $t(n) = O(n \log n)$
* If $\beta > 2$: $t(n) = O(n^{\log_2 \beta})$
## 1.1 MST in linear time
Setting:
- [[Weighted Graph]]
- See runtimes in [[MST Algorithms]]
- $w$ injective

T MST $\Leftrightarrow$ all edges in $e \in (E \setminus E_T)$ are [[T-heavy]]

We use **FindHeavy** as an algorithm to find all T-heavy edges in time $O(m)$.



