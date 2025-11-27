Deal with [[Aliasing (Objects)]].
## Benefits
- Better than coding guidelines to not leak pointers.
- Languages can leverage non-aliasing guarantees for memory management, thread synchronization, ...
## Drawbacks
- [[Aliasing (Objects)]] can be useful to share side effects
	- e.g. share that some properties are modified
	- Restricting access to shared objects via [[Readonly References]] can be enough.
## In C++
[[Unique Pointers (C++)]]
## In Rust
[[Ownership (Rust)]]
