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
#### 2-Manifold
A surface is a closed 2-manifold if it is locally homomorphic to a disk everywhere.
$\forall x$ point in $M$ $\exists B_{x}(r)$ open ball of radius $r>0$ centered at $x$ s.t. $M \cap B_x$ is homomorphic to an open disk.
![[Locally homomorphic to a disk.png]]
#### Manifolds with a boundary
A vicinity of each boundary point is homomorphic to a half-disk.
### Topology
#### Genus
Definition: Maximum number of cuts along non-intersecting simple closed curves without disconnecting the manifold.

$\Rightarrow$ How many holes? One closed curve through each hole.
#### Counting faces
[[Euler-Poincaré Formula]]
### Triangulation
Polygonal mesh where every face is a triangle (except the outer face when in 2D).
## Storage
### Independent Faces
Each face lists its vertex coordinates. Not used.
### Vertex and Face Tables
* Faces list vertex references
* Vertex table contains coordinates

Has shared vertices, but bad adjacency information.
### Adjacency Matrix
$A_{ij} = 1$ iff $\exists$ edge between vertex $i$ and $j$.

Pros: No topology assumption, meaningful eigenvectors, $(A^{n})_{ij} =$ \#paths of length $n$ from $i$ to $j$.
Cons: Storage (sparse matrix), no connection between face and vertex.
### Adjacency Lists
Store all vertex, edge and face adjacencies.

Has shared vertices and adjacency, but stores too much.
### Half Edges
Store lists of:
* Half-edges with pointers:
	* Twin half-edge
	* Next half-edge
	* Next vertex
	* Incident face
* Face with pointer:
	* 1 adjacent half-edge (arbitrary)
* Vertex with pointer:
	* 1 outgoing half-edge (arbitrary)

Pros: Adjacencies in $\mathcal{O}(1)$, good storage, arbitrary polygons
Cons: **Assumes 2-manifold** surfaces!
