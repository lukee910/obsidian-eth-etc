## 1 - Generics
[[Generics]], [[Contravariant]], [[03V Types pt. 2#Parameter Types]]
- `X<A> </: X<B>` and vice versa [[Java Generic Wildcard]]
	- Needs `X<? extends A>`
- `X<B> <: X<? extends B>`
## 2 - Type Erasure
[[Java Type Erasure]]
## 3 - Information Hiding
Idea: `B extends A`. B calls `this.foo`. B has public method. A has default method, default is more specific.
## 4 - Unique
[[Unique References]]
## 5 - Ownership
[[Ownership (Rust)]]
How can we call a method `foo(T val)` if we have a variable of type `&T`? Answer: We can't. Example is given in the `clone_string` method of how this is achieved (i.e. [[Ownership (Rust)#Unsafe Rust]] cloning).
## 6 - Non-Null Types and Initialization
[[_T Non-Null Initialization]]
