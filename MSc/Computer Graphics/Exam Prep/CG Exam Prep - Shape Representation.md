[[_T Shape Representation]]

## Tangents and Normals
![[Parametric Shapes#Parametric Tangents and Normals]]

## Implicit and Parametric Surface Equivalence
$f(x,y,z)$ and $s(u,v)$, show that they are the same:
- $\Rightarrow$: Substitute $(x,y,z)$ for $s(u,v)$ and show that $f(x,y,v)=0$, i.e. that parametric surface is contained in implicit surface
- $\Leftarrow$: Show that if $f(x,y,z)=0$, there exists $u,v$ such that $(x,y,z) = s(u,v)$, i.e. implicit surface is contained in parametric surface.
## Implicit Surface Boolean Operations
- $f \cup g == min(f, g)$
- $f \cap g == max(f, g)$
- $f \setminus g == max(f, -g)$
## Euler-Poincaré
[[Euler-Poincaré Formula]]: $\chi(M) = v - e + f$ 

In particular: For [[Polygonal Meshes#Genus]] $g$, we have $\chi(M) = 2 - 2g$
![[Polygonal Meshes#Genus]]

