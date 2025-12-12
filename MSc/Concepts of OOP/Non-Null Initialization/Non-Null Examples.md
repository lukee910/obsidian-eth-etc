## Works

### Cyclic Data Structures
Slides 6 Slide 42 (split out slide 145-157)

Cyclic structure initialization works, because we walk through the structure and set pointers, we get a steadily increasing set of [[Locally Initialized]] objects. In the end, everything is [[Transitively Initialized]].

See [[Non-Null Object Construction]].
### Lazy Initialization
Slides 6 Slide 47 (split out slide 175-177)

Idea: Initialize data only when we access it.

Solution: Private nullable field. Public non-null getter that initializes field if required (via null check).
## Problems
### Method Calls Revisited
Slides 6 Slide 43 (split out slide 158-161)

- Slide 158:
	- Cannot call committed method `optimalSize` from constructor
- Slide 159:
	- Invalid override in `Sub`
- Slide 160:
	- [[Contravariant]] [[Overriding]] is okay, however still has an issue.
- Slide 161:
	- Cannot access unclassified field on free `this` (field is possibly null)
		- Could check for null first

Problem: Escaping from a constructor means the object is still under construction, while you may enter code that is unaware of that.
### Call Backs Revisited
Slides 6 Slide 44 (split out slide 162-168)

- `this`/`Observer! o` is free when `register` is called from constructor
- Need to make `update` free too
- `this.data` breaks like in [[#Method Calls Revisited]]
### Escaping via Calls Revisited
Slides 6 Slide 45 (split out slide 169-172)

- `this`/`Observer! o` is free when `register` is called from constructor
- Problem: Cannot add a free object to a committed list
	- Storing free objects in a list is a bit nonsensical anyways
- Solution: First initialize object, *then* register.
	- Letting objects escape is a bit of a bad idea anyways.
### Escaping via Fields Revisited
Slides 6 Slide 46 (split out slide 173-174)

- `after.next = this` cannot be done, if left is committed then right must also be committed.
- Idea: We can't place an object in construction into an existing, running data structure.
	- Müller: This is a brittle way of programming anyways.

