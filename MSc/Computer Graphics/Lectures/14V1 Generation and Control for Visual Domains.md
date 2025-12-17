Generative AI shenanigans.

https://artificialanalysis.ai
Ranking of models in different domains. Very dynamic, moves all the time.

What is generative AI? Predicting a distribution of correct answers, not a single answer like with reconstruction.

Two issues: Training and Control
## Training
### Intrinsic
One or few inputs, try to reproduce that.
### Supervised
Data as answer.

Problem:
- Needs a lot of data
- Can only reproduce "regular" things
### Foundational
Train one model, show this everything you can. Then, adapt it to different tasks (distilling).

Problem:
- Needs the whole internet and a chunk of money
	- Academia depends on industry to train these models, need budget
### Distilling
The process of adapting a foundational model to a specific task. Get the right data out of it.
## Control
Previously: GANs, such as StyleGAN. Fine control, but limited knowledge.
Now: Diffusion Models. Know a lot of data, but super finicky.
### Motion Generation / Animation
Motion: Joint angles $\mathbb{R}^{3 \times J \times T}$
	- $J$ joints
	- $T$ tendons

Human Motion Diffusion (2023). From Bermano's lab, go to for motion synthesis.

Guiding: Human Motion Diffusion as a Generative Prior (2024).
Idea: Draw lines for certain joints, put those as a Gaussian prior.

CLoSD (2025): Bridge gap between generation as physics.
Idea: Predict a really short window, give this as input to physics sim. Do the next prediction of actual sim input.
### 2D Images
LDM (An Image is Worth One Word: Personalizing Text-to-Image Generation using Textual Inversion) (2022): Describing can have its issues. Control via images can have more concrete inputs.
Idea: Add a special token to embed object awareness. Show it a few images and name it "\<\*\> X".
### Exploration
{?} (2024?)
Idea: Decompose image into multiple concepts hierarchically.
### Attention
(is all you need)
Idea: Signal is decomposed into three descriptors:
- Keys
	- What is in that pixel?
- Queries
	- What other patches are of interest?
- Values
	- What is the value of the pixel?

Can combine keys of one image and queries plus values of other. Allows some re-targeting.

Practilight (2025):
Light transfer fails at the moment. In self-attention, the relation between two pixels is the relation of their light. Isolate the light from the scene to enable relighting on a much smaller model.
### 3D Shapes
(see slides, mentioned some models)

