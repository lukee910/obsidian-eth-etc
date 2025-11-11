## Radical Inverse
#TODO: Slides 17 Slide 47
## Van der Corput Sequence
#TODO: Slides 17 Slide 48
This generates a gap filling sequence. This sequence converges to $\mathcal{O}(\frac{\log N}{N})$.
## Halton Sequence
Expand the radical inverse sequence / [[#Van der Corput Sequence]] to multiple dimensions.

Idea: Do the radical inverse on relatively prime bases.

Result: A well distributed placement that does *not* require the number of samples in advance.

Problem: There's nothing random about this, we get [[Aliasing]]!
## Sequence Scrambling
Idea: Scramble the deterministic sequences to get rid of regularities. Can be applied very simply.

Q: Why does this not reintroduce the clumping? A: It's not actually random, the scramble factor is constant. So it's not really random.
## Convergence Rate
#TODO: Slides 17 Slide 63-65

