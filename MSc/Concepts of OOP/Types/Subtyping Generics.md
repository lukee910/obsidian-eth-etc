[[Generics]]
Same as with list / pointer pointer subtyping issues, must not be [[Subtyping|subtypes]].

Invariant. Neither [[Covariant]] nor [[Contravariant]].

i.e.
`List<Student> </: List<Object>`
## Approaches
- Add more type parameters (e.g. for return type)
	- `class TreeSet<F, E extends F>` ...
- [[Java Generic Wildcard]]
For a comparison, see [[Java Generic Wildcard#Example: Cell]] example.
