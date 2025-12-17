## Setup
All OOP languages support multiple [[Subtyping]]. Some also support multiple inheritance (e.g. C++, [[Scala traits]], ....).
## Problems
- Ambiguities
	- Same name methods in different superclasses
- Repeated inheritance (diamonds)
## Inheriting fields multiple times
$\Rightarrow$ C++ virtual inheritance / Eiffel default: Only keep one, the fields "override" into one.
Eiffel renaming or C++ default: Two fields are created, have to disambiguate.
## Initialization
*Non-virtual inheritance*: Constructor of multiply inherited superclass is called twice, via both paths.
*Virtual inheritance*: Smallest subclass calls the constructor directly, only once.

NOTE:
- Even if you go through non-virtual paths, if a class is inherited virtually once, it is only ever virtually inherited
- This applies even if one path inherits it non-virtually
## Resolving Issues
Accessing fields:
```c++
class A { int x; }
class B { int x; }
class F : public A, public B { }
void client() {
	F *f = new F();
	cout << f->x; // Issue!
	cout << f->A::x; // Works
}
```