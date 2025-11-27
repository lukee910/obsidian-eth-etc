[[Readonly References]]
See also: [[Ownership (Rust)]]
```rust
// Mutable
fn getAddr(&mut self) -> &mut Address {
	&mut self.addr
}

// Immutable
fn getAddr(&self) -> &Address {
	&self.addr
}
```

As soon as an immutable reference / immutable borrow is created, the original reference becomes immutable until all borrows have expired!
## Shared References
Multiple immutable references to a value may be created. All are valid simultaneously.
## Effectiveness
Safety is guaranteed:

```rust
struct Address { city: String, }
impl Address {
	fn getCity(&self) -> &String
	{ &self.city }
	fn setCity(&mut self, s: String)
	{ self.city = s }
}

struct Person { addr: Address, }
impl Person {
	fn getAddr(&self) -> &Address
	{ &self.addr }
	fn setAddr(&mut self, a: Address)
	{ self.addr = a; /* moves a */ }
}

// Run
fn m(p: Person) {
	let a = p.getAddr();
	
	// Both make a runtime error:
	a.setCity(String::from("Hagen"));
	a.city = String::from("Hagen");
}
```
## Transitivity
Transitivity works:
#TODO: Example Slides 5 Slide 77
## Readonly on Mutable Values
Mutable values become immutable while a immutable borrow exists. Doesn't hold for "Underlying objects remain mutable" in [[Readonly References#Requirements]].

```rust
struct Address { city: String, }
struct University { prof7: &Address, }

fn m(p: Person) {
	let mut a = Address{city: String::from("Zurich")};
	let u = University{prof7: &a} // create immutable borrow
	a.city = String::from("Winterthur"); // compile-time error
	let c = &u.prof7.city;
	// Immutable borrow expires here
}
```
## Discussion
- Effectiveness and Transitivity is given
- "Underlying objects remain mutable" is not given
	- Objects are immutable while they have an immutable borrow
	- Limits the uses in data structures
- Works well for library classes
