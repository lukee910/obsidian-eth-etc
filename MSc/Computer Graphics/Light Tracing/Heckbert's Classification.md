Classification of vertices on a [[Light Path]]:
## Notation
### Vertices
- L: Light source
- E: Eye
- S: Specular reflection
- D: Diffuse reflection
### Regex-Style Paths
- $k+$: One or more of event $k$
- $k*$: Zero or more of event $k$
- $k?$: One or one of event $k$
- $(k|h)$: A $k$ or $h$ event
## Example
- [[Direct Illumination]]: $L(D|S)E$
- [[Indirect Illumination]]: $L(D|S)(D|S)+E$
- [[Global Illumination]]: $L(D|S)*E$

Some paths:
![[Heckbert's Classification Examples.png]]
