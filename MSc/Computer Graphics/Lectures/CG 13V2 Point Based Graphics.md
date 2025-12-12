## Approach
Idea: Point generalizes the pixel.
## Representation
How to represent the surface?
### Surface Model
Discrete set of point samples gets mapped to surface interpolation.

Done with:
### Moving Least Squares
Idea: Given a point. Get a "surface" with the least squares approximation of the nearest points. Weigh points closer to the given point higher. Then, project the point onto that approximation.

This gives an infinitely smooth surface.

Variations exist, especially for easier computation.

Problems:
- Loss of details
- Unstable fit
### Spherical MLS
Idea: [[#Moving Least Squares]], but instead of fitting to a first order function, project onto algebraic sphere.

Much more stable.

Problems:
- Does not preserve corners, edges, sharpness
### Kernel Regression
Local Kernel Regression

Yet another statistical technique, gets smoothness and sharpness.
### Local Surface Analysis
Idea: Via Eigenvalues, fit an ellipsoid onto the surface.
## Resampling
Resolution can be incredibly high. How do we sample more in areas where it is needed and less in others?

Idea: Resample more in high curvature areas.
### Particle Simulation
Simulate repelling particles over the surface. Ends up in a Poisson disc sample of the surface.

Thing is, after repelling, you have to re-project the particles onto the surface (e.g. via [[#Moving Least Squares]]).
### Local Error Metric
Idea: Start with dense mesh, calculate error when removing any given point. Is this point important?
## Tools
### Pointshop 3D
Parametrize points locally by fitting a local plane onto the point where an effect is applied. Resample that local area, then apply a brush (for example).

Problem: You always need to reparametrize to apply an effect. One approach is the Constrained Minimum Distortion Parametrization.
### Paint Transfer
Haptic painting system with a simulated brush.

Idea: Embed appearance and geometry together, so this could be better.

Note: Paint buffer can create more points, by sampling the points onto a paint buffer and then resampling the paint buffer onto the surface.

Note: This can handle a lot of variation in levels of detail, since you can just create very dense points.
## Multi-Scale Modeling
(Skipped)
## Rendering
Note: Representation is very complex, but the frame buffer is not. Conceptually, typical triangles in complex 3D models project to <1 pixel.
### Surfels
"Surface pixels". Points store several surface attributes.
### Forward Projection
Idea: Project primitives onto the frame buffer. Both for triangles and for points.

Issues:
- Holes if not dense enough
- Texture and edge aliasing
### EWA Splatting
Not sure what this was about.
### Warping Reconstruction Kernels
Dealing with anti-aliasing.

Uses Gaussian reconstruction kernel in point space, projected onto screen space. This works out to Gaussian splatting.
### Ray Tracing
[[#Moving Least Squares]] is a projection operator, can be used for closeness to surface.
## Notes
Master Thesis: Rendering points from a modern perspective? EWA splatting, ray tracing, ...
