![[Subtyping Immutable vs Mutable.png]]
How to set a [[Subtyping]] relationship?

TL;DR clean solution is to have two separate classes, cannot use [[inheritance]] easily.

Alternatives:
1. Common superclass
2. [[Aggregation]]
3. [[Inheritance]] without [[Subtyping]]
	1. Can be done in C++ (also Eiffel)
4. Java's Collections
	1. `AbstractCollection` and `Iterator` are mutable
	2. All mutating methods are optional by convention. Good luck!

