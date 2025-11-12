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