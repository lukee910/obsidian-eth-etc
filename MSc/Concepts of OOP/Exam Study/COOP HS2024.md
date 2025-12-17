## 1 - Multiple Inheritance
[[Multiple Inheritance#Initialization]]
## 2 - Ownership Types in Rust
[[Ownership (Rust)]]
## 3 - Subtyping
[[Subtyping]], [[Behavioural Subtyping]], [[Structural Subtyping]]
### 3C
Subtype relations:
- `B <: A`
- `C <: interface { A f(C) }`
- `D <: C`
## 4 - Generics
[[Generics]]
[[Subtyping Generics#Scala: Variance Annotations]]
## 5 - Non-Null Types
[[_T Non-Null Initialization]]
[[Non-Null Types]]

NOTE: `if (x == null) {return} x.foo()` only works if `x` is local, because of concurrency!

[[Transitively Initialized]]