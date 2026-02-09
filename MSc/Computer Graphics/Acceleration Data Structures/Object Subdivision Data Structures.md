* Preprocess
	* Decompose space into disjoint regions
* Rendering
	* Traverse through regions overlapping the ray
	* Intersect objects only in each region until hit

[[Ray-AABB Intersection]] is very fast, so mostly use [[Axis Aligned Bounding Box]]'s.
## Grids
### Uniform Grids
Uniform voxel grids of fixed resolution (often $\sim 3\sqrt[3]{n}$).

Preprocessing: Store objects in grid
Traversal: Efficient algo without divisions (Bresenham’s algorithm).

Pros: Easy to code
Issues: Scaling (lots of empty space), scenes are not uniform.

### Hierarchical Grids
e.g. 2-level grids, make two granularities.

But, also just a patch on a patch.
## Trees
* octree (uniformly subdivide nodes)
* kd-tree (adaptive sizes, AABB, most common)
* bsp-tree (binary spatial partition, non-trivial traversal)
### Kd-Tree
Binary tree with variable volume sizes.

Example:
![[Split with Midpoint.png]]

Stores nodes:
* Internal nodes:
	* Split axis ($\in$ x, y, z)
	* Split position (coord on the axis)
	* Children: 1-2 child nodes
* Leaf nodes
	* List of primitive pointers

Construction:
* Compute bounding box
* Recursively split cell using axis-aligned plane
	* Choose split axis
		* e.g. alternate (x, then y, then z (if available))
		* e.g. longest axis
		* e.g. widest spread (which axis divides the elements the best)
		* Often use longest, because it makes balanced cells $\to$ less intersections.
	* Choose split point
		* e.g. midpoint
		* e.g. \#primitives
		* e.g. [[Surface Area Heuristic]] (SAH)
	* Until termination criteria
		* e.g. max depth
		* e.g. min \#objects

### Octrees
Similar to [[Object Subdivision Data Structures#kd-tree]].

Recursively subdivide cells into 8 equal sub-cells. Until termination criterion.

Less efficient, but cheaper for insertion and deletion of elements.

### General BSP-Trees
Like kd-trees, but not axis aligned. Too expensive to traverse, usually.
## Bounding Volume Hierarchy BVH
Decompose objects into (overlapping) sets and bounds of simple volumes for fast rejection.

Usually spheres as the primitives.

Top-down vs bottom up: Usually, **use bottom-up**

Top down: Make a big bounding box, subdivide.
![[BVH top down.png]]
Bottom up: Individual boxes per primitives, bunch them together.
![[BVH bottom up.png]]
