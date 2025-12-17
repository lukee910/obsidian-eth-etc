## Notes
### Task 2 - Generics
[[Generics]]
- Make sure to check all methods and fields accessed
### Task 3 - Bytecode Verification
Rules: [[Bytecode Verification via Type Inference]]
### Task 4 - Multiple Inheritance
[[Multiple Inheritance]]
- Make sure to create more instantiable classes than less if needed
#### Virtual Inheritance
```c++
public class Sub : virtual public Super1, virtual public Super2 { }
```
This makes sure that member fields are only inherited once.

NOTE: This does *not* make sure that *methods* are only inherited once!
For that, use:
- Overrides / virtual methods.
- Add a method in the `Sub` class of the same signature, that disambiguates.
### Tasks 5-6 - Not part of content