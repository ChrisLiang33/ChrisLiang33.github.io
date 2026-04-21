---
title: "Brain Hemorrhage Detection with DDPM Reconstruction"
excerpt: "Using a diffusion model trained only on healthy brain scans to detect hemorrhages via reconstruction error."
collection: portfolio
---

**Course:** Generative AI, Fall 2025

We investigated whether a Denoising Diffusion Probabilistic Model (DDPM) trained solely on "healthy" images could be used for anomaly detection in medical imaging — the idea being that reconstructing an unhealthy image would produce a noticeably worse reconstruction than a healthy one.

**What we built:**

- Trained a UNet-based DDPM (64 base channels, channel multipliers (1,2,4), 1000 timesteps, linear β schedule) on clean images.
- Validated the approach on a synthetic MNIST corruption benchmark (AUROC **0.93**).
- Scaled to brain CT scans for hemorrhage detection, comparing a from-scratch ~30M parameter model against a pretrained ~114M parameter variant.

**Findings:**

- Diffusion models are decent at image-level anomaly detection but weaker at pixel-level localization.
- Pretrained models achieved lower validation reconstruction error but were actually worse at anomaly detection — a reminder that the training objective and the deployment task aren't always aligned.

**Stack:** PyTorch, Hugging Face Diffusers.

*Collaborators: Dennis Loevlie, Roger Brockett.*
