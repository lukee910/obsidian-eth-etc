[[Readonly References]]

C++ `const` pointers guarantee:
- No field updates
- No mutator calls
	- Via [[`const` Functions]]

Note: `const T* <: T*`
## Basic Example
```c++
class Address {
	string city;
public:
	string getCity() const {
		return city;
	}
	void setCity(string s) {
		city = s;
	}
}
class Person {
	Address* addr;
public:
	const Address* getAddr() {
		return addr;
	}
	void setAddr(Address a) {
		/* clone */
	}
}

// Run:
void m(Persopn *p) {
	const Address* a = p->getAddr();
	a->setCity("Hagen"); // compile-time error
	cout << a->getCity(); // call of `const` function allowed
}
```
## Downcasts
Note: `const` pointers can be down-cast to normal pointers. No run-time check!
```c++
void m(Person *p) {
	Address *a = (Address *)p->getAddr();
	a->setCity("Hagen"); // Works
}
```
## Transitivity
Transitivity is not applied. `const` has to be (manually) applied down the entire tree.
## Pros & Cons
### Pros
- Readonly access to mutable objects
- Works for library classes
- Supports arrays, fields, non-public methods
### Cons
- Not transitive
- Unsafe
	- Via explicit casts
- Does not prevent [[Aliasing (Objects)#Capturing]]
