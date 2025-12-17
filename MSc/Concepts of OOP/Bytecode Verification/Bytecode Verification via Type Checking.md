Motivation: [[Bytecode Verification via Type Inference]] is slow. Extend class file to store type information.

Type information is the required state of the stack and registers `(S, R)` at the beginning of any basic block:
- Jump target
- Entry point of exception handler
- Includes any join point

Uses the same rules as [[Bytecode Verification via Type Inference]]
