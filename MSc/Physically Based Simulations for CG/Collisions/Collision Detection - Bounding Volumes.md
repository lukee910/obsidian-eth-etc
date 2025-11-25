Idea: Do easy negative intersect checks cheaply.
## Bounding Volume Types
### Sphere
Overlap test: $|c^{1} - c^{2}| < (r^{1} - r^{2})$

Properties:
- Cheap
- Potentially bad shape approximation
### Axis Aligned Bounding Box
[[Axis Aligned Bounding Box]]

Overlap test: Project box onto each axis, do an integer range intersect check on each. Intersects if it intersects on each axis.

Properties:
- Cheap
- Okay shape approximation
### Oriented Bounding Boxes
Overlap test: Separating Axis Theorem. Provide an example separation.

Properties:
- Complicated to test
- Good shape approximation
## Bounding Volume Hierarchies
[[Object Subdivision Data Structures#Bounding Volume Hierarchy BVH]]
Idea: Subdivide volumes recursively to get a better shape approximation.

