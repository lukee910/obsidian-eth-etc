## Recap
* Weak vs Strong Typing
* Structural vs Nominal Typing
* Static vs Dynamic Type Checking
## Overriding
### Parameter Types
```
class Super {
	void food(String s) {}
	void bar (Object o) {}
}
class Sub <: Super {
	void food(Object o) {} // ok
	void bar (String s) {} // nok
}
```
Perspective: Given client code on super, can the sub handle everything?

$\Rightarrow$ **Contravariant Parameters**: Overriding must not require more specific parameter types.

Overloading vs Overriding: Can cause ambiguity, e.g. Java does not allow overriding with different parameters (it's automatically overloading then).
### Result Types
```
class Super {
	Object food() {}
	String bar () {}
}
class Sub <: Super {
	String food() {} // ok
	Object bar () {} // nok
}
```
Perspective: Given client code on super, can it handle the sub returns?

$\Rightarrow$ Contravariant results
(Also applies to exceptions, out parameters, ...)
### Fields
```
class Super {
	String f;
	Object t;
}
class Sub <: Super {
	Object f; // cannot be read by client code on Super
	String t; // client code on Super can write too much in here
}
```
Fields have to be read and written $\Rightarrow$ contravariant and covariant $\Rightarrow$ cannot be overridden.

What if we make it immutable?
Problem: It has to be initialized! E.g. super constructor can write too much to covariant sub field.
## Covariant Arrays
Problems if you allow it.

C#, Java allow covariant arrays, which causes type issues (runtime check at each array update).
## Shortcomings of Nominal Subtyping
* If classes were not developed to be subtypes, you can't change that
	* e.g. similar classes from different libraries
	* Possible Solution: Adapter Pattern
### Optional Methods in Java
Java convention: In documentation mark methods optional. Implementations can then throw exceptions in these methods.
## Structural Subtyping and Substitution
Subtype objects and understand at least the messages the supertype can. Have wider interfaces by definition.
## Contracts
Used here to document behaviour (not required for examples shown here)
### Method Contract
* Preconditions
	* Notes as: `// requires`
* Postconditions
	* Notes as: `// ensures`
	* Both parameters and state
* Old-expressions
	* Noted as: `old(x)`
	* Refer to pre-call heap when in the post condition
		* Global state
		* Object fields
		* NOT: Parameters, local variables

Note: Parameters only have one version, the one initially passed. The outside never sees, if that version is locally modified.
### Object Invariants
`// invariant a == b`
Invariants have to hold in all states after construction, in which an object can be accessed by other objects (visible states). Invariants may be violated temporarily during executions, only have to hold in pre- and poststates of methods.

Pre- and poststates are the visible states.
### History Constraints
`// constraint old(age) <= age`
History constraints relate visible states (with old-expressions). Must hold for any two visible states (must be transitive and reflexive).
### Contract Checking
* Static checking
	* Formal verification, Code reviews
	* Pros
		* Static Safety
	* Cons
		* Complex
		* Large overhead
			* Need to make extensive, detailed contracts
* Dynamic checking
	* Run-time assertions
	* Pros
		* Efficient bug-finding
		* Partial contracts can be fast
	* Cons
		* Expressiveness: Not everything can be properly checked (e.g. Is an array sorted? Too expensive to check every visible state!)
## Contracts and Subtyping
### Rules for Subtyping
Subtype objects must fulfill contracts of supertypes.
#### Preconditions
Only weaker.
#### Postconditions
Only stronger.
#### Invariants
Only stronger.
#### History Constraints
Only stronger.
#### Overriding Methods of Subtypes
Weaker preconditions.
Stronger Postconditions.