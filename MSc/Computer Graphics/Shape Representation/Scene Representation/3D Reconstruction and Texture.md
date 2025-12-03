Problem: Novel Scene Generation
Given: 2D images from multiple angles
Output: Novel view
## 3D Reconstruction
Recall: [[3D Reconstruction - Overview]], we can get the geometry.
## Texture Mapping
Mapping between the reconstructed surface and the image.

Some issues:
- Don't want to blur (e.g. by averaging from all images)
- Have to consider lighting
### Optimization Formulation
Idea: Minimize the texture difference for each image.
#TODO: Formulas slide 23-26
$$
\min\sum\limits_{i} \|  \|
$$
### Issues
- Lambertian surface assumptions
- Errors in the geometry and calibration mess with things
- Issues with UV mapping
	- Especially at the seams
	- Ptex tries to deal with this
- Need to account for various things
	- View dependent effects
	- Motion in the scene
	- Lighting
### Neural Approach
[QUADify](https://studios.disneyresearch.com/2024/06/05/quadify-extracting-meshes-with-pixel-level-details-and-materials-from-images/)
