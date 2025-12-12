## Well-Typed
`new C(e_i)` is [[Well-Typed]] if:
- All `e_i` are [[Well-Typed]]
- Class `C` contains a constructor with suitable parameter types
## Type
Type of `new C(e_i)` is:
- [[Non-Null Committed Type]] `C!` if the static types of all `e_i` are committed
- [[Non-Null Free Type]] otherwise
