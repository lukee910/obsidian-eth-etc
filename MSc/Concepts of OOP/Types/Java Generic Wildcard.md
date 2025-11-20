[[Generics]]
Existential type: `<?>`

Idea: Generics can be restrictive, make the the type flexible. Keep information by using [[#Constrained Wildcard]]s.

Useful example: [[#Example Tree Set with Wildcards]] (similar to actual implementation).
## Types Visible
e.g.:
`static Collection<?> id(Collection<?> c) { return c; }`

Definition side: Existential type. Is there a type that fulfills this type declaration? If yes, we compile.

Note: Each existential type is independent.

Client code: Considers the `?` as its [[Type Upper Bound]] (in Java: Object, similar to `unknown`).
i.e. for `id(ArrayList<String>)`, we still get `Collection<?>` as the return type, not `Collection<String>`.
## Constrained Wildcard
`? extends T`

Then we get back some information. Not unknown, but considered the same as its [[Type Upper Bound]] / lower bound.
### Wildcard Lower Bound
`? super T`

Same as before, but defines `T` as a lower bound of `?`.
## Use-Site Variance
### Use-Site Covariance
[[Covariant]]
With [[Type Upper Bound]].
```Java
class Random<T> {
	T next() { /*...*/ }
	void initialize(T i) { /*...*/ }
}

Random<? extends Person> r = new Random<Student>();
r.initialize(new Person()); // ok, ? <: Person
r.initialize(new Student()); // does not compile, ? </: Student can be the case
```
### Use-Site Contravariance
[[Contravariant]]
With [[#Wildcard Lower Bound]].
```Java
class OutputChannel<T> {
	void write(T x) {};
	T lastWritten() {}
}

OutputChannel<? super Student> o = new OutputChannel<Person>();
o.write(new Student()); // Student <: Person, so the method parameter contravariance holds.
Person s = o.lastWritten(); // Doesn't hold, all we know is that ? <: Object (any supertype of Student)
```
## Versus Method Type Parameters
### Equivalencies
[[Type Upper Bound]]:
```Java
// equivalent:
void copyFrom(Cell<? extends T> other) {}
<S extends T> void copyFrom(Cell<S> other) {}
```
[[#Wildcard Lower Bound]]:
Not possible:
```Java
<S super T> void copyFrom(Cell<S> other) {} // does NOT compile
```
### Expressiveness
```Java
class Wrapper {
	Cell<?> data;
}
class Wrapper<T> {
	Cell<T> data;
}
```
`Wrapper` can change type, `Wrapper<T>` is constantly typed per instance.
## Subtyping
[[Subtyping]]

The bounds for a wildcard determine the set of *possible instantiations*. (For normal generics, that set has a single element, namely that concrete type)

For types S and T with the same class or interface (if `T` and `S` not the same class, then walk up to common ancestor), S is a subtype of T if for each type argument the set of possible instantiations for S is a subset of the set of possible instantiations for T.

i.e.: `S <: T` if  #TODO: Slides 4 Slide 59
## Decidability
Note: Java with wildcards is not decidable. Without them, it is decidable.

Note: Prof. Müller says wildcards are not worth the complexity.

#TODO: Code on slide 60

Q: `C<T> <: N<? super C<T>>`?
$\Rightarrow$ `N<N<? super C<C<T>>>> <: N<? super C<T>>`

// Now we have the same class on both sides, apply [[#Subtyping]] logic $\Rightarrow$ is `C<T>` a subtype of instantiation `N<? super C<C<T>>>`?

$\Rightarrow$ `C<T> <: N<? super C<C<T>>>`
$\Rightarrow$ `N<N<? super C<C<T>>>> <: N<? super C<C<T>>>`
$\Rightarrow$ `C<C<T>> <: N<? super C<C<T>>`

After each iteration of the above, we add one more `C<T>` to the left type.

Note: The type checker has to invent types that do not appear in the program, and can create infinitely many of them (leading to the infinite loop).
## Examples
### Example: Spooler
```Java
class Spooler {
	Collection<?> task;
	
	void setTask(Collection<?> c) {
		task = c;
	}

	void print() {
		for (Object e : task) {
			System.out.println(e);
		}
	}
}
```
Note: `task` can change type across runtime (on same instance).
### Example: Cell
```Java
class Cell<T> {
	T value;
	
	void copyFrom(Cell<T> other) {
		value = other.value;
	}
	
	void copyFrom(Cell<? extends T> other) {
		value = other.value;
	}
}
```
Note, this is equivalent to:
```Java
void copyFrom<U>(Cell<U extends T> other) {
	value = other.value;
}

Collection<int>
```
### Example: Tree Set with Wildcards
```Java
interface Comparator<T> {
	int compare(T fst, T snd);
}
class TreeSet<E> {
	TreeSet(Comparator<? super E> c) {}
}

class Person {}
class Student extends Person {}

class PersonComp implements Comparator<Person> {}

TreeSet<Student> s = new TreeSet<Student>(new PersonComp());
```
