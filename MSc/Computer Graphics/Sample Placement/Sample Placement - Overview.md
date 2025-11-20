## Idea
Place samples within a pixel more cleverly.
## Approaches
### Random Sampling
Problem: Some places are oversampled, others have no information.
### Regular (Grid) Sampling
Problem: [[MSc/Computer Graphics/Sample Placement/Aliasing]]
### Stratified Sampling
[[#Regular (Grid) Sampling]], but randomize the placement of samples within the grid.
![[Stratified Sampling.png|200]]
#### Stratified Problem: Dimensionality
Problem: Stratification requires $N^{d}$ samples (curse of dimensionality). Inconvenient for large $d$.

Solution: Compute stratified samples in lower dimensions and randomly combine. #Unclear
![[Stratified sampling higher dimension.png]]
#### Stratified Problem: Clumping
Problem: Clumping can still happen. Per axis (project all points onto an axis), stratified sampling is a random distribution. Not stratification per axis.

Solution: [[#N-Rooks Sampling]]
#### Jittered Sampling
alias for [[#Stratified Sampling]]
### N-Rooks Sampling
Idea: Each row and column on a grid has one point in it. This improves the clumping

Calculation: One point per row, shuffle rows. Then, shuffle all columns.
#### N-Rooks Problem: Gaps
Problem: Gaps are still happening.
#### Latin Hypercube Sampling
alias for [[#N-Rooks Sampling]]
### Multi-Jittered Sampling
Idea: Combine [[#Jittered Sampling]] and [[#N-Rooks Sampling]].

![[Stratification Overview.png]]
![[Multi-Jittered Sampling.png|250]]
#### Multi-Jitter Problems
- Some clumping remains
- Needs to know the number of samples a-prior
### Low-Discrepancy Sampling
Low-Discrepancy sampling is a big field, we look at one approach: [[Sequences for Sampling]]. [[Sequences for Sampling#Halton Sequence]] with [[Sequences for Sampling#Sequence Scrambling]].

#TODO: List of stuff on Slides 17 Slide 61
## Implementing
Warning: Rate of improvement as $N$ increases can be misleading. When implementing, start with uniform sampling, only then add Quasi-Monte Carlo.

If you know the number of samples, just do some form of [[#Stratified Sampling]] etc.. If you don't, use [[#Low-Discrepancy Sampling]].
