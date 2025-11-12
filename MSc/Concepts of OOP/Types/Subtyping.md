A <: B $\Leftrightarrow$ A is a subtype of B

Subtype objects can understand at least the messages that supertype objects can understand. Notably, applies to fields and methods.

More conceptual vs [[Inheritance]]

## Wider Interfaces
Subtype objects need to understand at least the messages that supertype objects can.

For:
- Method calls
- Field accesses
It must hold that:
- Existence: Fields and methods must exist
- Accessibility: Must be at least as accessible
- Types: Methods and fields must fulfill certain subtyping relations.
	- [[03V Types pt. 2#Overriding]]
