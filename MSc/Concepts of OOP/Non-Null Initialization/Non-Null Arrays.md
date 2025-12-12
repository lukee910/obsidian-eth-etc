Arrays are objects whose fields are numbered.
## Reference Types
Two kinds of references:
- Reference to array object
- References to the array elements
- Both can be non-null or possibly-null
```Java
Person![]! a;
Person?[]! b; // Non-Null array with possibly-null elements
Person![]? c; // Possibly-Null array with non-null elements
Person?[]? d;
```
## Array Initialization Problem
### Problem
Our solution for non-null fields *does not work* for non-null array elements. For example, how do you initialize values in a loop?

Initialization is not done in array constructor, but in a loop.
### Solutions
#### Array Initializer
```C#
// Spec#
String![]! s = {“array”, “of”, “non-null”, “String”};
```
Problem: Only sometimes works.
#### Pre-filling the array
```Eiffel
my_array: attached ARRAY[attached STRING]
create my_array.make_filled(“”, 1, l)
```
Special method `make_filled`: Pre-initialize from index `1`, length `l`, fill it with `""`.

Problem: How is `""` better than `null`? Arbitrary behaviour but you don't even get an exception for it. Probably worse than `null`.
#### Runtime checks
```C#
// Spec#
free String![]! s = new String![l];
for(int i=0; i<l/2; i++) { /* as before */ }
NonNullType.AssertInitialized(s);
```
Special runtime check that ensures array non-null. After this type of method call, the array is considered non-null.

This is equivalent to returning from the `new` expression, but manually tell the compiler when it happens.
##### Equivalent Formulation
Can think about it in the following way:
```C#
String![]! s = new String![l] {
	for (int i = 0; i < l / 2; i++) {
		// as before
	}
} // == NonNullType.AssertInitialized(s);
```
