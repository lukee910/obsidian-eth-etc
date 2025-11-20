## Idea
Problem: Complex models take a long time to simulate.

Solution: We don't need all these degrees of freedom. Find a low-dimensional subspace that captures desired behaviour, simulate there.

Goals:
- Faster than full model
- Cost independent of full model complexity
- Similar behaviour to full model
## Simple Variant - Linear Modal Analysis
[[Linear Modal Analysis]]

Improvements:
- [[Subspace Simulation with Nonlinear Forces]]
- PCA Basis #TODO
- Modal Derivatives #TODO
- Machine learning: Learn the subspace
	- Give it examples of deformations
	- Subspace structure will be terrible
## Simulation Setup
[[Subspace Simulation Basics]]
