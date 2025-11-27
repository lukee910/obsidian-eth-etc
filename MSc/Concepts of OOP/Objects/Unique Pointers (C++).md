Library solution for [[Unique References]].

`make_unique<T>(c)` creates a `unique_ptr<T>`, which wraps the actual pointer.
```c++
// Example: T = Address
unique_ptr<Address> zurich = make_unique<Address>("Zurich");
```
NOTE: When a unique pointer gets destroyed, it automatically deallocates the underlying object.
## Methods Overview
- `make_unique<T>()`: constructor ([[#In C++]])
- `std::move()`: destructive read ([[#Ownership Transfer]])
- `unique_ptr<T>.get()`: non-destructive read ([[#Switching Back To Regular Pointers]])
## Protecting Uniqueness
Uniqueness is protected by deleting the copy and assignment constructor (`return addr; addr = a` are both prevented).
## Ownership Transfer
`std::move()`, destructive read. Automatically destroys the moved unique pointer.

```c++
void test(unique_ptr<Address> a) {
...
}

test(std::move(zurich)) // This disallocates `zurich`
test(std::move(zurich)) // !! This crashes (deallocated)
```
### Temporary Ownership Transfer
#### Transfer: Unique Pointer Pointer
Use `unique_ptr<Address>*` as a method parameter:
```c++
void test_temp(unique_ptr<Address>* a) {
...
}

test_temp(&zurich)
test_temp(&zurich) // This still works
```
Problem: This again allows aliasing.

This is what is most commonly used in C++ :/
#### Transfer: Unique Pointer Structs
Safer alternative to [[#Unique Pointer Pointer]]: Return all unique pointers in a struct:
```c++
Triple compare(unique_ptr<Address> a, unique_ptr<Address> b) {
	Triple r; // int res; unique_ptr<Address> a, b;
	r.res = a->getCity().compare( b->getCity() );
	r.a = std::move( a ); r.b = std::move( b );
	return r;
}
```
Problem: This creates overhead and is rarely used for that reason.

This actually prevents aliasing.
## Switching Back To Regular Pointers
`unique_ptr<T>.get()` returns a regular pointer `T*`. Aliases can be created.

This is a non-destructive read! vs `std::move()` [[#Ownership Transfer]].
## Problems
### Operations within object
Any method call inside the object loses the information that it's supposed to be a unique pointer. Aliases can easily be created there:
```c++
static Address* cache;
class Address {
	// Address is unaware that it's not supposed to make aliases
	string getCity() { cache = this; return city; }
}

class Person {
	unique_ptr<Address> addr;
	string getCity() { return addr->getCity( ); }
}
```
### Dangling Pointers
Destroying a unique pointer deallocates the underlying object, *even if* an alias exists:
```c++
Address* returnAlias() {
	unique_ptr<Address> a;
	a = make_unique<Address>("Zurich");
	return a.get();
	// a is destroyed here, as scope ends.
	// Address underlying is destroyed.
}
Address* a = returnAlias();
// Return value is a dangling pointer, as object is NULL
cout << a->getCity(); // !! Crashes
```
### Shallow Ownership
Unique pointers only give you shallow ownership. i.e. only the first level is actually owned. Any referenced objects can still be aliased. Any referenced objects will not also automatically be destroyed on destroying the unique pointer.
![[Shallow Ownership.png]]
## Pros & Cons
### Pros
- Unique pointers express design intent
	- Does not guarantee uniqueness
- *Direct* leaking or capturing is prevented statically
- Memory manager is simplified
	- Still requires care
### Cons
- No static guarantees
- Not effective in solving [[Aliasing Problems]]
- Parameter passing is awkward
- Destructive reads are error prone
