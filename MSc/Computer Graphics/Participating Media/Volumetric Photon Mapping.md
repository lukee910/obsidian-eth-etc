As with [[Photon Mapping]], but deposit photons in the volume. Do the [[Free-Path Sampling]] to get interaction points as with [[Volumetric Path Tracing]].

Use deposited photons as the in-scattered radiance.

Can get volumetric caustics.
## Step Size Problems
- Can find photons multiple times
- Miss photons with large step size

Solution: Beam Radiance Estimate. (Slides 16 Slide 146)
