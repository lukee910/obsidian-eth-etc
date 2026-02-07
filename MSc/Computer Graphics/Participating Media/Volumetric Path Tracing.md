## Idea
As [[Path Tracing]], but paths can:
- Reflect/refract off surfaces
- Scatter inside a volume (*this is new*)

Process:
1. Sample distance to next interaction
2. Scatter in the volume OR bounce off a surface
![[Volumetric Path Tracing.png]]
With [[Next Event Estimation|NEE]]:
![[Volumetric Path Tracing NEE.png]]
## Scattering Direction
Sample proportional to [[Phase Function]]: [[Phase Function#Sampling]].
## Finding the next Interaction
[[Free-Path Sampling]]
## Dealing with the next Interaction
Once we have an interaction, decide if we want to cancel the ray or if we want to scatter based on [[Absorption Coefficient]] and [[Scattering Coefficient]].
