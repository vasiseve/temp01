# Summary of rebuttal

## The post-rebuttal version includes the following main revisions, available at the rebuttal_revision_845.pdf:

- Rewrote the introduction to clarify the paper’s logic earlier and more explicitly
- Reframed the paper around two tested hypotheses:
  - circulation as a diagnostic of local path dependence / non-integrability
  - SSR as a diagnostic of local perturbation amplification
- Stated the main empirical finding up front: circulation is detectable but weakly predictive, while SSR is strongly predictive of fixed-\(x_t\) semantic disagreement
- Replaced/improved the opening qualitative figure with clearer DDIM/DDPM disagreement examples from the same anchor
- Added the overview schematic of the full fixed-\(x_t\) protocol
- Reorganized the method section into clearer components:
  - circulation
  - SSR
  - scalable estimation
- Added an explicit clarification that exact-score Jacobians are symmetric, but our diagnostics are computed on the learned field actually integrated during sampling, so the antisymmetric component is not zero by definition
- Added a formal appendix discussion/proposition on exact-score symmetry vs. learned-field geometry
- Narrowed the main claim around the DDPM–DDIM setting and clarified that this comparison is a stress test of local perturbation amplification, not a pure discretization-only comparison
- Clarified that deterministic–deterministic solver comparisons are supportive breadth/generalization evidence rather than the main validation setting
- Made the statistics setup more explicit
- Added feature-extractor sensitivity checks beyond ResNet-18:
  - CLIP image embeddings
  - LPIPS
- Added appendix discussion showing that the main SSR–disagreement pattern persists under these alternative semantic metrics
- Added runtime / overhead measurements for SSR estimation
- Clarified the intended use of SSR as a targeted diagnostic rather than a default online per-step method
- Revised the circulation discussion to avoid implying an absolute “zero” threshold; it is now interpreted relative to the conservative-control / estimator-floor baseline
- Softened and clarified the interpretation of the semantic-vs-pixel asymmetry
- Clarified the interpretation of the E4 strain/rotation regression, especially the meaning of the negative rotation coefficient
- Promoted a compact cross-solver / cross-model generality summary into the main paper
- Calibrated the wording around generality to avoid overstating deterministic-only and latent-space results
- Added an explicit Limitations section
- Rewrote the conclusion to emphasize the paper’s main conceptual separation: path dependence vs. amplification
- Added related work on diffusion path variance / dynamical analysis
- Cleaned and reorganized the appendix structure for clarity
- Improved figure captions and presentation for readability and takeaway clarity
- Standardized terminology around SSR, strain, and rotation/spin
- Improved notation introduction so key symbols are defined earlier and more clearly

## Figure 1

![Figure 1](Figure_1.png)

**Figure 1.** Qualitative examples of fixed-\(x_t\) cross-sampler disagreement. For the same intermediate noisy anchor, DDIM and DDPM can produce semantically different final reconstructions. These examples illustrate the phenomenon studied in the paper: sampler families are not always interchangeable even when initialized from the identical state.

## Main paper schematic

![Main paper schematic](Figure_main.jpeg)

**Main paper schematic.** Overview of the experimental pipeline. Starting from a shared anchor \((x_t, t)\), we first compute two local geometry diagnostics before running any sampler:
- **Circulation \(C_n\):** a diagnostic of local path dependence / non-integrability
- **Strain-to-Spin Ratio (SSR):**  
  \[
  \mathrm{SSR}(x,t)=\frac{\|S(x,t)\|_F}{\|\Omega(x,t)\|_F+\epsilon}
  \]
  used as a predictor of downstream solver disagreement

We then run different samplers from the same anchor and measure the resulting cross-sampler semantic disagreement between the reconstructed outputs.
