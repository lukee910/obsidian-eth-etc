Implementing [[Java Security]] for [[JVM Bytecode]].
## Overview
[[Bytecode Verification Overview#Proper execution requires]]
[[JVM]] guarantees these properties via bytecode verification on load and dynamic checks at runtime.

Compiler also helps, by we don't trust that in this setup.
## Approaches
At runtime, use one of the following approaches:
- [[Bytecode Verification via Type Inference]]
- [[Bytecode Verification via Type Checking]]