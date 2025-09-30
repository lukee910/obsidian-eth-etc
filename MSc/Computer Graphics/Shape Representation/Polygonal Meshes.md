## General
* We always use triangles
* Error is in $O(h^{2})$, $h$ faces.
## Definitions
Vertices $v_0,\ldots,v_{n-1}$, Edges $\{ (v_{0}, v_{1}), \ldots, v_{n-2}, v_{n-1} \}$.
### Closed Polygon
$v_{0}= v_{n-1}$
### Simple
Not self intersecting, no two edges share a common vertex except the endpoints.
### Polygonal Mesh
$M = <V, E, F>$. A set $M$ of closed, simple polygons $Q_i$. Each $Q_i$ defines a face.
The intersection of two polygons $Q_{i}, Q_{j}$ is either empty, a vertex, or an edge.
### Manifolds
In a manifold mesh, there are at most 2 faces incident to any edge and each vertex is a manifold vertex.

A manifold vertex has a 1-connected ring of faces around it (in particular, they are not disconnected by removing said vertex, no pointy shapes).