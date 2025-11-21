## Definition
An object `o` is aliased if two or more variables hold references to `o`.
### Variables
Possible variables that reference to an object can be:
- Fields
	- Instance and Static
- Local variables
	- Including `this`
- Formal parameters of method executions
- Results of method calls and other expressions
## Why
- Efficiency
	- Do not need to copy objects when passed or modified
- Sharing
	- State can be modified from multiple locations
## Creating (unintended) aliases
[[#Capturing]] is often done intentionally, [[#Leaking]] is usually a mistake.
### Capturing
Objects are passed to another object and then stored (i.e. captured). A new alias is created.

Problem: Alias can be used to bypass interface. [[Aliasing Problems#Example Bypassing Interface]]
### Leaking
Object passes a reference to an object that is supposed to be internal.

Problem: Access and modification to internal state. Client can bypass our object's interface.

