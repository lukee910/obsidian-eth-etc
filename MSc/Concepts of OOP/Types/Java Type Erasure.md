## Why
Backwards compatibility with older versions of [[JVM]] when introducing generics in Java.

C# added proper generics in the bytecode, so do not have to do this.
## Idea
[[Generics]] type information is erased by the compiler.
- `C<T>` is translated to `C`
- `T` is translated to its upper bound
- Casts are added where necessary
- Only one classfile and only one class object represents all instantiations.
## Example
### Generics
```Java
// -- Generic Class
class Cell<T extends Object> {
	T value;
	void set(T v) {
		value = v;
	}
	T get() {
		return value;
	}
}
// Becomes:
class Cell {
	Object value;
	void set(Object v) {
		value = v;
	}
	Object get() {
		return value;
	}
}

// -- Client Code:
Cell<String> c;
c = new Cell<String>();
c.set("Hello");
String s = c.get();
// Becomes:
Cell c;
c = new Cell();
c.set("Hello");
String s = (String) c.get(); // Added cast!
```
### Common Supertype
[[COOP HS2021#1B]]: Inferred types are the least common superclass? #Unclear : Example.
## Implications
At runtime, we do not know the type information of generic classes!

Impossible:
- `c instanceof Cell<String>`
	- `c instanceof Cell` works
- `Cell<String>.class`
	- `Cell.class` works
- `new Cell<String>[10]`
	- We do not have the type of information to do the runtime type checks for covariant arrays [[03V Types pt. 2#Covariant Arrays]].
## Overloading
Type erasure can create duplicate method signatures:
```Java
class Erasure<S, T> {
	void foo(S p) {}
	void foo(T p) {} // Problem!
}
```
If the upper bound is different, this works (as other types are inserted):
```Java
class Erasure<S, T extends Person> {
	void foo(S p) {}
	void foo(T p) {}
}
```
## Static Fields
Static fields are shared by all instantiations of a generic class. Static fields cannot be of a generic type for that reason.
