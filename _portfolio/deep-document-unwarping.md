---
title: "Deep Document Unwarping"
excerpt: "Rectifying non-rigidly deformed document images with a Vision Transformer-based pipeline that predicts a dense UV coordinate map."
collection: portfolio
---

**Course:** Computer Vision, Fall 2025

Unlike planar document rectification which can be solved with a single homography, crumpled and folded pages require pixel-wise displacement estimation. This project designed a deep learning pipeline to rectify such non-rigid deformations.

**What was built:**

- Vision Transformer backbone to reason about 3D document geometry from a single crumpled input image.
- Prediction head outputting a dense UV map — a per-pixel lookup table into the flat, rectified document.
- Differentiable warping layer resampling the input image through the predicted UV map to produce the final output.
- Trained on a synthetic dataset of deformed documents (~8.6 GB).

**Stack:** PyTorch, OpenCV, Hugging Face Transformers.
