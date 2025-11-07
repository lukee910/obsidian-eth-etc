## Idea
As Path Tracing, but paths can:
- Reflect/refract off surfaces
- Scatter inside a volume (this is new)

Process:
1. Sample distance to next interaction
2. Scatter in the volume OR bounce off a surface
![[Volumetric Path Tracing.png]]
With NEE:
![[Volumetric Path Tracing NEE.png]]
## Scattering Direction
Sample proportional to [[Phase Function]]: [[Phase Function#Sampling]].
## Finding the next interaction
[[Free-Path Sampling]]