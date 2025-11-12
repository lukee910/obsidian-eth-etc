[[Static Method Binding]]
[[Dynamic Method Binding]]
## Pros and Cons
[[Dynamic Method Binding]] allows specialization and subtype polymorphism, however has some drawbacks for performance and versioning.
## Differences in practice
### Java
Searches the most specific method declaration. Adding a method to a supertype can make the subtype method not be called!
### C\#
Choose the most specific method class of the receiver, then the superclass, ...

