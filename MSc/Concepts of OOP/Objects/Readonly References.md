## Requirements
- Underlying objects remain mutable
	- Immutable is property of reference only
- Effectiveness
	- No way of  bypassing this
- Transitivity
	- Apply restriction to sub-objects.

Note: Any examples in the slides where the address is "Hagen" is an example of what shouldn't happen. Your address should never be Hagen.
## Via Supertypes (Java)
Idea: Leak it only as `ReadonlyAddress`

```java
interface ReadonlyAddress {
	public string getStreet();
}
class Address implements ReadonlyAddress { /* .. */ }

class Person {
	private Address addr;
	public ReadonlyAddress getAddr() { return addr; }
	public void setAddr(Address a) { addr = a.clone(); }
}
```
Problems:
- Cast allows modification
	- It's not safe!
- Transitivity needs to be explicitly encoded everywhere
	- What if `ReadonlyAddress` had a field of type `LinkedList<String>`?
- Libraries may not have a readonly interface
	- Have to implement everything yourselves, perhaps
- Java: Not everything can have an interface, e.g. arrays and fields
## Via `const` Pointers (C++)
[[`const` Pointers]]
## Immutable References (Rust)