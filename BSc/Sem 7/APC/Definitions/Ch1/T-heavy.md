---
mathLink:
---
#NoteType/Definition 
#CompSci/Theoretical/Algorithmics/Graphs 

## Symbol

T-heavy ^symbol
## Definition

Given a spanning tree $T = (V, E_T)$, every edge $e \in E,\ e \notin E_T$ will close a unique cycle.
We call $e$ **T-heavy** iff $\forall e' \in E_T\ w(e') < w(e)$ ^definition

Note: If it is not a spanning tree (e.g. in a spanning forest), we call any edge that closes a cycle T-heavy regardless.

