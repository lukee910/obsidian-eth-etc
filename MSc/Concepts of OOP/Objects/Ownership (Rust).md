[[Unique References]] built into the Rust language from the start.
## Owned Values
By default, values in a memory location (a "place") are owned exclusively by the containing type. Nobody else can access it, it's not alias-able pointers by default.

Basically, everything is local exclusive by default. Everything is on the stack by default.
![[Rust Owned Value.png|200]]
## Type Box
Type Box provides owning pointers to heap-allocated variables.
![[Rust Type Box.png|300]]
This is rust's way of allocating on the heap. Used for more long-lived values. Ownership still applies.
## Ownership Transfer
- When reading from a place, ownership is transferred
- Every assignment is a move assignment

Note: This means, that when a value is passed as a parameter, it cannot be used anymore thereafter:
```rust
fn createPerson(a: Address) -> Person {
	Person { addr: a }
}
//
let a = Address { city: String::from("Zurich") };
let p = createPerson(a);
let q = createPerson(a); // !! Compile time error: use of moved value
```
## Borrowing
Temporary [[#Ownership Transfer]].

Idea: I want to retain ownership, but want to lend this to the other function. While borrowed, ownership is lost and the field is inaccessible!

This is done via prefixing `&` to the variable (ignore the `mut` here, see [[Immutable References (Rust)]]):
```c++
fn compare(a: &mut Address, b: &mut Address) -> Ordering {
	a.getCity().cmp(b.getCity())
}
let mut a1 = Address {/*..*/};
let mut a2 = Address {/*..*/};
let o = compare(&mut a1, &mut a2);
let c = a1.getCity(); // Can still use it here
```

Note: When borrowing a field, the other fields remain accessible by the original value:
```rust
let mut p = Person::new();
let a = &mut p.addr;
println!("{}", p.name); // Can work, despite the addr borrow
println!("{}", a.city);
// Borrow a expires here
```
### Borrow and Temporary Aliasing
Borrowing creates a temporary alias that makes the original way of accessing the variable unusable until borrowing is done.

Example for borrowed value being unable to be used:
![[Rust Borrow Original Unusable.png]]
Other way around (`println!("{}", a.city); println!("{}", p.addr.city);`) works.
### Borrow Checker
Compiler does a static analysis to detect when borrows start and end.

Borrow checking across function may require annotations (lifetimes, not discussed here).
#### Borrow Expiration
Borrows expire whenever they are used last.
## Guarantees
### Simplified Uniqueness Guarantee
Rust guarantees that, in each execution state, there is at most one usable place that can access a value.

Rust uses this guarantee for:
- Data race freedom
- Automatic memory management
### Leaking and Capturing
[[Aliasing (Objects)#Leaking]]: Rust does not prevent (temporary) leaking through a reference.

[[Aliasing (Objects)#Capturing]]: Safe, since the ownership is properly transferred. Caller cannot use the value any longer.
## Shared References
Note: With [[Immutable References (Rust)]], shared references can be created.
## Consequences
### Using `mut`
Using `mut` gives explicit permission to the client to mess with your state.  Have to think what this means when using this.
### Memory Management
Automatic memory management in Rust is safe. When a place goes out of scope, all values it (transitively) owns are automatically deallocated.
This includes [[#Type Box]], since if you own the box, nobody else does, even if it's on the heap.
### Exchanging Implementations
[[Aliasing (Objects)#Capturing]]:
Creating an alias via Capturing is prevented, so the array creation example is safe. Can change implementation, since nobody can edit elements from outside anyways.
```rust
struct List {
	array: Vec<i32>,
	// can replace with linked impl.:
	head: Box<Node>,
}
setElems(&mut self, ia: Vec<i32>) {
	self.array = ia;
}
```
[[Aliasing (Objects)#Leaking]]:
Creating an alias via leaking is still possible. Leaking and non-leaking methods typically have different result types.
![[Rust Leaking Exchanging Impl.png]]
## Limitations
### Invariants
Since [[Aliasing (Objects)#Leaking]] is possible, clients can bypass our invariant:
```rust
struct List {
	array: Vec<i32>,
	// invariant
	// \forall i. 0 <= i < array.len():
	//     array[i] >= 0
}

fn violate(l: &mut List) {
	let a = l.getElems();
	a[0] = -1;
}
```

[[Immutable References (Rust)]] can help with safe leaking.
### Tree-Shaped Data Structures
Implicitly, all data structures must be tree-shaped. No cyclic data structures!
![[Rust Tree Structures Limitations.png]]
#### Unsafe Rust
Gives access to raw pointers that do not do ownership and borrowing. Then, it works similar to C++ pointers.

Idea: Confine unsafe code in very clear locations, encapsulated inside libraries. Limit the impact of it.
## Pros & Cons
### Pros
- Ownership guarantees a form of uniqueness
	- Because of [[Immutable References (Rust)]], this is called "Aliasing XOR Mutability"
- Creating aliases via capturing is prevented statically
- Automatic memory safety and data race freedom
- 0 runtime overhead

Note: Many languages are building in ownership at the moment.
### Cons
- Leaking still possible
- Not effective in solving all [[Aliasing Problems]]
- Ownership is strict, need [[#Unsafe Rust]]
- Guarantees may be compromised by using [[#Unsafe Rust]]
