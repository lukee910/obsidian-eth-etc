## Idea
Find points of interest in image and match them between images.

Interesting points:
- Well-defined position in image space
- Stable under local and global perturbations
- Efficient to detect
## Keypoint Detection
Goal: Get [[Feature Descriptor]] for different keypoints.
### Detection Approaches
#### Image Derivatives
E.g. Change of brightness
#### Boundary Extraction
E.g. Edge detection, Harris corner.
## Matching
### Create Mathces
Use a Structure From Motion (SFM) algorithm.
### Handling Outliers in SFM
[[Random Sample Consensus]]
### Bundle adjustment
When you have found things for multiple cameras, how can you make sure that the positions agree?

We don't look at this, but there's an algorithm for nudging the 3D points and cameras around a bit.
