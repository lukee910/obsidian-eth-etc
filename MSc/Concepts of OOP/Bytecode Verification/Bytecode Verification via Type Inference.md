Bytecode verifier simulates the execution of the program, but operations are performed on types instead of values.

Must be fast, since this is executed at runtime.
## Instruction Rules
For each instruction, we have a rule of its types. E.g.:
```
// S: defines the structure of the stack
// R: defines the registers
i: (S, R) -> (S', R')
// iadd takes two ints from the stack and puts one back
iadd: (int.int.S, R) -> (int.S, R)
```
### Special Notation
- `MS`: Maximum Stack Size
- `MR`: Maximum number of registers/local variables
- `R(n)`: Type of the value in that register. E.g.: `R(n) = int` to check the register type.
- `R{n <- t}`: Register `n` is updated to type `t`
Those are stored in the classfile.
### Invocation
Invocation uses the method signature, doesn't include the actual jump.
### Examples
```
iconst n:
(S,R) -> (int.S, R), if |S| < MS

iload n:
(S,R) -> (int.S, R), if 0 <= n < MR AND R(n) = int AND |S| < MS

astore n:
(t.S, R) -> (S, R{n <- t}), if 0 <= n < MR AND t <: Object

invokevirtual C.m.sigma:
(t'_n. .. .t'_1.t'.S, R) -> (r.S, R), if sigma = r(t_1, ..., t_n) AND t' <: C AND t'_i <: t_i
```
## Finding Errors
Errors are denoted by the absence of a transition rule that could be applied. Either a type mismatch or Stack over-/underflow.
## Types Available
- Primitive types
- Object and array reference types
- `null` for a null reference
- `T` "top" for uninitialized registers
![[Bytecode Verifier Types.png]]
## Full flow example
![[Bytecode Type Inference Example.png]]
## Multiple Predecessors
Motivation: Jumps may lead to joins in control flow. Instructions have several predecessors.
![[Smallest Common Supertype Example.png]]
