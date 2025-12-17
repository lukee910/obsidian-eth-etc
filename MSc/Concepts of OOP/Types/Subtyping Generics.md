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
## Scala: Variance Annotations
```scala
// Covariance: +
class Random[+T] {
	def next: T = {/**/}
}
// ok: OutputChannel[String] <: OutputChannel[AnyRef]
val r: Random[AnyRef] = new Random[String]()
val a = r.next

// Contravariance: -
class OutputChannel[-T] {
	def write(x: T) = {/**/}
}
// ok: OutputChannel[AnyRef] <: OutputChannel[String]
val o: OutputChannel[String] = new OutputChannel[AnyRef]()
o.write("Hi")
```

Type parameter can only appear where the corresponding type of variance is allowed (see [[03V Types pt. 2#Overriding]]):
- [[Covariant]]
	- Result Types
	- Immutable Fields
- [[Contravariant]]
	- Parameter Type