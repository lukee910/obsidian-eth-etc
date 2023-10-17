#CompSci/Theoretical/Algorithmics 
#ETH/BSC/S2/AnW
#CompSci/Theoretical/Algorithmics/Graphs

## Boruvka's Algorithm

### Pseudocode
- $\forall\ v \in V$: compute $e_{min}(v)$, insert $e_{min}(v)$ in the MST and contract $e_{min}(v)$, producing $G/e_{min}(v)$ (removing loops and double edges by keeping only cheapest edge)
- Recurse (until the graph contains only one vertex)

### Runtimes
- Time: $O(m \log n)$
	- Per iteration: $O(m)$, expected number of iterations: $O(\log n)$
- Space: 

## Prim's Algorithm
### Runtimes
- Time: $O(n \log n + m)$
	- Using Fibonacci heaps
- Space: 

## Kruskal's Algorithm

### Runtimes
- Time: $O(m \log n)$
	- Using union find data structure
- Space: 