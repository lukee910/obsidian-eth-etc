Ambiguity resolution for [[Multiple Inheritance]]. For example for [[Scala Traits]].
## Linearization Rules
For class or trait `C extends C' with C1 ... with Cn`
The linearization is defined as: $L(C) = C, L(Cn) \cdot \ldots \cdot L(C_{1}) \cdot L(C')$
### Operations
- $\varepsilon \cdot B = B$
	- Remove empty
- $(a, A) \cdot B = a, (A \cdot B)$ if $a \notin B$, otherwise $= A \cdot B$.
	- Keep rightmost
## Resolving a Linearization
Approach:
1. Write the `C,C' DOT ...`
2. Flatten all of them separately
3. Remove redundant, keep right
#TODO: Example slide 87
