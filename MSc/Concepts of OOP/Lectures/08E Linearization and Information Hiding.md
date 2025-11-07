Sheet 7: Linearization and Information Hiding
## Task 1
Find all the types that can be created with or without traits, as well as the subtype relations between them.
```scala
class C
trait T extends C
trait U extends C
class D extends C
```
We can make:
```scala
C
C with T // == T (in a set sense), since T extends C
C with U // == U
// (A) are equivalent _type wise_. Behaviour may be different!
C with T with U // (A)
C with U with T // (A)

// Same for D:
D
D with T
D with U
D with T with U
D with U with T
```
Subtype relations: Diamond shape diagram, but two of them interleaved. Turns into a 3D cube.
## Task 2
Trait order shenanigans (aka linearization).
### A)
- `a` normal cell, `b` normal with increment
- `c.set(5) == 11` 2i+1
- `d.set(5) == 12` 2(i+1)

Dot operator: Applies the linearization, final linearization only has commas.
### B)
Will not work.
- Why?
	- Removes duplicate types.
- What does it do?
	- Not compile / double once.
- How to make it work?
	- Make `trait Doubling2 extends Doubling {}`?
		- No, this actually directly goes to `Doubling`, who's super is `Cell`
	- Make `trait Doubling2 extends Cell { override set(i:Int) {..} }`
		- Works, since `Doubling2` is not skipped by usual override mechanics as before
	- Make a proper quadrupling trait
## Task 3
Output of main?

Note: First check that it actually compiles!

Linearization:
- L(...) = A, L(B) . L(C) . L(D)
- = A, B, A, C, B, A, D, B, A (insert all)
- = C,D,B,A (remove dupes)

=> BDC
Note the concatenation order is super first, then add your own.
## Task 4
### Classes
- `Person`
- `Student`
- `PersonWithLicense <: Person`
### Traits
- `Gardener <: Person`
- `Lawyer <: Person`
- `TaxiDriver <: Person`
### Self Type Annotation
Validate whenever these traits are mixed in that it actually is mixed onto the selected class.
Note:
- Behaviour is different (`super` is *not* the checked type)
- Has the methods, but not the type
### Task
#### A.1
Linearization $\Rightarrow$ "working in court in Zurich"
#### A.2
Doesn't compile: `Gardener` requires `Person`, which `Student` isn't.
#### B
Needed:
- "in the garden" at the end, need a `Gardener` at the end
- "in Zurich" so `TaxiDriver` before `Gardener`
- "not", so we need a negated `hasValidLicense`. `this.hasValidLicense()` needs to be something below `Lawyer`. `Gardener` cannot since it's not a `PersonWithLicense`, so we override it in `TaxiDriver`.
- `PersonWithLicense` because we need that, of course
So we get:
`new PersonWithLicense with Lawyer with TaxiDriver with Gardener`. Add method in `TaxiDriver`: `override def hasValidLicense(): Boolean = { return false; }`
## Task 5
- `Buyer <: Person`
- `SmartBuyer <: Buyer`
Give the most restrictive access modifiers that still is compiled. `public > protected > default > private`
- `protected tickets`
- `/*default*/ maxTickets`
- `inc()`
	- `Buyer`: `private`
	- `SmartBuyer`: `private`
- `buy()`
	- `Person`: `default`
	- `Buyer`: `public`
## Linearization
Approach:
1. Write the `C,C' DOT ...`
2. Do all of them separately
3. Remove redundant, keep right

For slide 87 example:
1. 