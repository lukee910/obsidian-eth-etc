## Setup
Two objects represented by triangle meshes $M^{1}(x^{1}, t^{1}), M^{2}(x^{2}, t^{2})$, with vertex vectors $x^{i}$ and triangle index vectors $t^{i}$.
A triangle $t_{j}^{i} = (k,l,m)$  is a triplet of integer indices into the vertex vector $x^{i}$.

Goal: Find all triangle pairs $(t_{i}^{1}, t_{j}^{2})$ that are intersecting.
## Complexity
$n$ number of faces.
Worst Case: $O(n^{2})$ [[#Naive Approach]]
Average Case:
- #TODO 
## Naive Approach
Test the triangles pairwise. There's nothing wrong, just slow ($\mathcal{O}(|t|^{2}$)).

Worst case, that runtime holds. We'll be improving the general case though.
## Broad and Narrow Phase
### Broad Phase
Use [[Collision Detection - Bounding Volumes|bounding volumes]] to compute potentially colliding triangle pairs ([[PCTP]]).
### Narrow Phase
Check if the [[PCTP]] intersect.
#### Approach 1 - Distance
Compute closest distance on that triangle pair ([[Triangle-Triangle Distance]]).
#### Approach 2 - Edge and Vertex Tests
[[Triangle Primitive Collisions]]

