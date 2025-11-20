## Idea
Parameterized classes and methods. Clients provide instantiations for template parameters.

C++'s approximation of [[Generics]]. 
## Generation
Purely a compile time construct, compiler generates a class for given instantiation.

Different instantiations of a template are completely unrelated, have no [[Subtyping]] associated with it.
## Type Checking
Template itself is not type checked with regards to generic parameters, only concrete instantiations are!

Note: The compiler *only type checks the methods that are actually used*. Errors in other methods will not appear! (See example on slides 04 slide 70)

No need for [[Type Upper Bound]], since they are ignored anyways :)
## Concepts
Something like [[Type Upper Bound]]

Concepts declare syntactic and type constraints.

Note:
- Concept requirements are checked for instantiations.
	- Template itself is still not type checked.
- Modularity issue persists
## Whacky Things
- Template parameters don't need to be types
- Templates can be specialized, specific instantiations
```C++
// Non-type parameter template
template <int n> class Fact {
public:
	static const int val = Fact<n-1>::val * n;
}

// Specialization, end recursion
template<> class Fact<0> {
public:
	static const int val = 0;
}
```

