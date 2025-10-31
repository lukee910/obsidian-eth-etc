Context: How the [[JVM]] does [[_T Bytecode Verification]].
## Stack vs Registers
- Most values are on the stack, not directly in the registers
- Registers store method parameters and local variables
## Bytecode
- Bytecode instructions are typed
- `_load` and `_store` access registers (e.g. `istore` for int store, `aload` for reference load)
- Control is handled with `goto`s, conditional branches, the usual stuff.
