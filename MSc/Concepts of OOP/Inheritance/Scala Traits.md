Traits can be mixed in during inheritance or object creation.

```Scala
class Cell {
	var value: Int = 0
	
	def put(v: Int) = { value = v }
	def get: Int = value
}

trait Backup extends Cell {
	var backup: Int = 0
	
	override def put(v: Int) = {
		backup = value
		super.put(v)
	}
	def undo = { super.put(backup) }
}

//

object Main1 {
	def main(args: Array[String]) = {
		val a = new Cell with Backup
		// ...
	}
}
```

Traits must:
- Extend exactly one superclass (and possibly other traits)
- Always be in reference to an object of a superclass (trait alone is not instantiable)
Traits may have:
- Fields
- Override methods
- Newly declared methods
## Traits and Types
Each [[Scala Traits]] defines a type. Trait types are abstract.
## Ambiguity Resolution
Traits are merged. Fields are no issue.
### Function: Non-Overriding
```Scala
class Professor {}

trait Assistant {
  var mentor: Professor
  def workLoad: Int = 6
}
trait Student {
  var mentor: Professor
  def workLoad: Int = 5
}Common

class PhDStudent
	extends AnyRef
	with Assistant
	with Student {}
// Issue: workLoad ambiguous!
```
Methods are unclear how to merge, have to manually resolve with:
- Add `workLoad` to super, make them an override (see: [[#Function With Override]])
- Override in `PhDStudent`:
	- `override def workLoad: Int = { super[Student].workLoad + super[Assistant].workLoad }`
### Function: With Override
If the different traits override a common supertype method, use [[Linearization]] to figure out what to do.
