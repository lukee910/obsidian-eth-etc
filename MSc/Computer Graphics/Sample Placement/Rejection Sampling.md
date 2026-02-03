Idea: Sample a larger domain and reject any samples not in the desired domain.
## Examples
### Disk
```c
Vec2 v;
do {
	// sample
	v.x = 1 - 2 * drand48();
	v.y = 1 - 2 * drand48();
// while sample invalid
} while (v.length() * v.length() > 1)
```
### Sphere
```c
Vec3 v;
do {
	// sample
	v.x = 1 - 2 * drand48();
	v.y = 1 - 2 * drand48();
	v.z = 1 - 2 * drand48();
// while sample invalid
} while (v.length() * v.length() > 1)
// Project onto sphere surface
v /= v.length();
```
Note: For hemisphere, sample sphere and then flip on appropriate axis if it's in the wrong hemisphere.
## Properties
Pros:
- Flexible
Cons:
- Inefficient
- Problems with low-discrepancy sampling

Used for: Complex shapes. If you have an analytical solution (See [[CG 04V2 Monte Carlo#Inversion Method Process]]), use that.