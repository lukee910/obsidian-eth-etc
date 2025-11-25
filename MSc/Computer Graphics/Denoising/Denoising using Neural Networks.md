Looking at the non-commercial version, can be downloaded.

Data driven denoising, got a Academy SciTech award in 2025. `Vogels et. al 2016` and follow-ups by DRS and Pixar/ILM.
## Overview
1. What should the network learn to do? [[#Objective]]
2. Which loss function should we use? [[#Loss Function]]
3. Can we exploit domain-specific knowledge? [[#Domain-Specific Knowledge]]
Other things to look at:
4. What constitutes a good training dataset?
5. What network architecture to use?
6. ...
## Objective
### Direct Prediction (Naive Way)
Input: Noisy image, feature buffers
Output: Denoised image
### Kernel-Predicting Networks
Output: Kernel weights

We do not know the optimal weights, but can still optimize for improved weights.
## Loss Function
- L1
- MAPE (Mean Absolute Percentage Error)
- MSE (Mean Squared Error)
- SSIM (Structural Similarity)

SSIM: Try to approximate perceptive difference, not absolute / value difference. MAPE and SSIM were the best in their experiments.

Choice of loss function is highly domain-specific. Try out loss functions!

In the end, they ended up using a different one, SMAPE (symmetric MAPE).
## Domain-Specific Knowledge
### Per-Component Denoising
For Disney BSDF, denoise per glossy and diffuse (which is then further separated into the albedo and irradiance components).
### Other Extensions
- Spatial-Temporal
- Multi-Scale Filtering


