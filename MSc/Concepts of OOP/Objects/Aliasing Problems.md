Many established techniques of OOP don't work for [[Object Structure]]s, only for individual objects.

E.g. [[Information hiding]]: Have to make things accessible to other objects in the structure, so it's public.
## Example: Bypassing Interface
Assume a list implementation based on arrays that takes an array and uses that as its data structure with [[Aliasing (Objects)#Capturing]]. The client still has an old reference to the list (which is array-based). Replace that with an implementation of a linked list and suddenly the old way of updating the list via the array directly doesn't work.

Observable behaviour has changed despite [[information hiding]].
![[Aliasing Bypassing Interface.png]]
## Invariants
[[03V Types pt. 2#Contracts]]: 
### Textbook version
Assumption: Every object `o` is a capsule:
- Only methods executed on `o` can modify `o`'s state
- The invariant of object `o` refers only to the encapsulated fields of `o`
#TODO: Rest of slides 5 slide 18
### Object adaptions
Assumption: The invariants of object `o` may refer only to private fields of `o`
#TODO: Rest of slides 5 slide 20

#TODO: Slides 5 slide 22
## Leaking
See [[Aliasing (Objects)#Leaking]].
