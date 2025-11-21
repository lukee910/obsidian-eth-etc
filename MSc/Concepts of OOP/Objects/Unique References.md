Deal with [[Aliasing (Objects)]].
## Benefits
- Better than coding guidelines to not leak pointers.
- Languages can leverage non-aliasing guarantees for memory management, thread synchronization, ...
## In C++
Library solution.
`make_unique<Address>(c)` creates a `unique_ptr`, which wraps the actual pointer.
### Protecting Uniqueness
Uniqueness is protected by deleting the copy and assignment constructor (`return addr; addr = a` are both prevented).
### Preventing Memory Leaks
When a unique pointer gets destroyed, it automatically deallocates the underlying object.
### Ownership Transfer
`std::move()`, destructive read. Automatically destroys the moved unique pointer.
