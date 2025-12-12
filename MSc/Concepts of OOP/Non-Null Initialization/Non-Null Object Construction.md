Constructing [[Non-Null Types]]. Idea: We only allow taking [[Non-Null Committed Type|committed]] arguments, so we don't get into trouble.
## Assumptions
- New-expression takes only committed arguments
- Nested new-expressions take arbitrary arguments
## After new-expression
- All new objects are [[Locally Initialized]]
- New objects reference only [[Transitively Initialized]] objects and each other
- All new objects are [[Transitively Initialized]]
## Proof-by-PowerPoint
Show that the [[#After new-expression]] statements hold.
### Legend
![[Object Construction Non-Null - Legend.png]]
### The simple cases
- Pointing in and out to the main type
	- Basically, only allow pointing out to [[Transitively Initialized]] types since stuff breaks otherwise.
- Construct a nested type that is easily a [[Non-Null Committed Type]]
![[Object Construction Non-Null - Simple Cases.png]]
### While not initialized yet
Here, we initialize the nested type to the right. By setting this arrow, we get that the nested type becomes [[Locally Initialized]].
![[Object Construction Non-Null - Not Initialized.png]]
### While circular nested type is initialized
Once the nested type is [[Locally Initialized]], return to the main type to finish its initialization.

After this, both the objects are only pointing to [[Locally Initialized]] objects, so they become [[Transitively Initialized]].
![[Object Construction Non-Null - Transitive pt 1.png]]
![[Object Construction Non-Null - Transitive pt 2.png]]
### Final state
Idea: It only saw [[Non-Null Committed Type]] from the outside or jointly initialized objects that all ran their constructor, terminating by being [[Locally Initialized]]. Since everything's either already committed or [[Locally Initialized]], everything becomes [[Transitively Initialized]].
![[Object Construction Non-Null.png]]
## Timing
![[Object Construction Non-Null - Timing.png]]
Everything is considered [[Non-Null Free Type]] until the termination of `new`. However, nested types have to be [[Locally Initialized]] after their new terminates.
