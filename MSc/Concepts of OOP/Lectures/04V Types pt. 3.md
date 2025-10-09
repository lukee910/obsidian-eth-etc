## Nominal Subtyping ff
### Checking Behavioural Subtyping
Static checking:
* Pre-Post Conditions
	* For each override method `S.m` of `T.m`, check for all parameters, heaps and results: (`Pre_T.m` $\Rightarrow$ `Pre_S.m`) && (`Post_S.m` $\Rightarrow$ `Post_T.m`) (attention on the order of those)
* Invariants and History Constraints
	* For each subtype S <: T check for all heaps: (`Inv_S` $\Rightarrow$ `Inv_T`) && (`Cons_S` $\Rightarrow$ `Cons_T`)
Dynamic checking:
* Not really done
* Check required properties at beginning and end of method execution
### Less restrictive type checking rules
`Post_S.m` $\Rightarrow$ `Post_T.m` can be a bit restrictive, can we also use the invariants or history constraints?

Add "`old(Pre_T.m)` $\Rightarrow$" to the start: `old(Pre_T.m)` $\Rightarrow$ `Post_S.m` $\Rightarrow$ `Post_T.m`

Not `Pre_T.m`, since that does not hold anymore at the post condition timing.
### Automatic checking of behavioural subtyping
Becomes undecidable very quickly, not really an option.
## Behavioural Structural Subtyping
Things are a bit different to what we had so far.

Cannot establish preconditions, have no postconditions to assume. Difficult.

In conclusion: Structural subtyping ignores behaviour!
### In Static Structural
Language could implement a feature that adds pre- and postconditions to the structural subtyping system. Behaviour as part of subtyping. But: This cannot be automated reliably.
## Subtyping Behaviour Conclusion
Nominal Static => Maximum static security
Structural Dynamic => Maximum flexibility

The other two corners have some issues:
Nominal dynamic: May as well do static
Structural Static: Problems with semantics of subtypes (and type equivalence)
## Types as Contracts
Types can be seen as a special type of contract, where static checking is decidable.

But: Contracts can be violated between visible states!
![[Types as Contracts.png]]
### Subtyping
Stronger invariant: Requires S' <: S
Weaker precondition: Requires T <: T'
Stronger postcondition: Requires U' <: U

$\Rightarrow$ we get a similar variance situation to subtyping, except for fields.
### Invariants over Inherited Fields
Invariants over inherited field f can be violated by methods that have access to f on super.

We can strengthen inherited invariants, but we cannot constrain the inherited fields further when strengthening!

This conflicts with "Stronger invariant: Requires S' <: S"!
## Inheritance
[[Inheritance]]
### Inheritance vs Subtyping
Subtyping expresses classification
vs
Inheritance is a means of code reuse

Inheritance is usually coupled with subtyping

Terminology: [[Subclassing]]

Note: Inheritance is **not a core concept**, OOP can be done without inheritance (subtyping + aggregation). Subtyping is a core concept, though! (Still useful)
#### Simulating Subclassing without Inheritance
![[Subclassing without Inheritance.png]]
### Immutable Example
TL;DR clean solution is to have two separate classes, cannot use inheritance easily.

Alternatives:
1. Common Superclass
2. Aggregation
3. Inheritance without Subtyping
	1. Can be done in C++ (also Eiffel)
