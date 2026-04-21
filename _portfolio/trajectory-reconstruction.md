---
title: "Probabilistic Trajectory Reconstruction from Keyframes"
excerpt: "Reconstructing high-frequency robot trajectories from sparse keyframes using Gaussian Processes and a masked variational autoencoder."
collection: portfolio
---

**Course:** Bayesian Deep Learning, Spring 2025

Robot trajectories recorded at high frequency produce large, bandwidth-heavy datasets. This project explored whether sparse keyframes could be used to reconstruct the full trajectory with calibrated uncertainty — useful for low-bandwidth control pipelines and uncertainty-aware motion planning.

**What we built:**

- **Baseline:** per-joint Gaussian Process regression over RBF and Matérn kernels, treating each joint independently.
- **Upgrade:** a masked variational autoencoder that encodes the entire trajectory with learned per-timestep mean and variance, using the keyframe mask to distinguish observed from imputed samples.
- **Evaluation:** compared both methods on MSE and credible-interval coverage across keyframe rates on a real SO-101 manipulator dataset (166 teleoperated block-picking episodes).

**Finding:** the VAE wins at sparse keyframe rates (≤ 1 Hz) by exploiting dataset-wide motion structure; the GP stays competitive at dense rates where local interpolation is sufficient.

**Stack:** PyTorch, NumPy, SciPy.
