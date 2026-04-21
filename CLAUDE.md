# Claude Code Brief — Academicpages Site Setup

## Context

This is a fork of `academicpages/academicpages.github.io` that will deploy to `chrisliang33.github.io`.

**Owner:** Xianmai (Chris) Liang — MS CS student at Tufts University, robotics research focus.

**Goal for this session:** Get a minimum viable personal academic site live tonight. Homepage, CV page, Research page, and 5 portfolio entries. Everything else (publications, talks, teaching) should either be emptied out or left as template placeholders that don't show in the nav.

**Audience:** research lab PIs, robotics industry recruiters (Figure, 1X, Rotor). Tone should be professional but not stiff.

---

## Owner facts (for config + author blocks)

| Field | Value |
|---|---|
| Full name | Xianmai (Chris) Liang |
| Preferred display | Xianmai (Chris) Liang |
| Email | xianmailiang@gmail.com |
| Location | Medford, MA |
| GitHub | ChrisLiang33 |
| LinkedIn | xianmai-liang-9b84b5253 |
| Site URL | https://chrisliang33.github.io |
| Degree | MS Computer Science, Tufts University (expected May 2027) |
| Prior degree | BS Computer Science, Brandeis University, May 2024, Magna Cum Laude |

**No Google Scholar, no ORCID, no Twitter, no publications yet — leave those empty or remove from nav.**

---

## Task list (execute in this order)

### 1. Edit `_config.yml`

Update the following keys. Leave everything else at template defaults.

```yaml
title: "Xianmai (Chris) Liang"
description: "Master's student in Computer Science at Tufts University researching safe and performant autonomous robotics."
url: "https://chrisliang33.github.io"
repository: "ChrisLiang33/ChrisLiang33.github.io"

# Author / owner block
author:
  name: "Xianmai (Chris) Liang"
  avatar: "profile.png"  # placeholder — Chris will drop a photo at images/profile.png
  bio: "MS CS @ Tufts. Robotics, learning, and control."
  location: "Medford, MA"
  email: "xianmailiang@gmail.com"
  github: "ChrisLiang33"
  linkedin: "xianmai-liang-9b84b5253"
  # Remove or leave blank: googlescholar, orcid, twitter, facebook, instagram, etc.
```

Also set `author.employer: "Tufts University"` if that field exists in the template.

### 2. Replace `_pages/about.md` body

Keep the frontmatter. Replace the body with:

```markdown
I'm a master's student in Computer Science at Tufts University, currently researching safe and performant autonomous robotics in the [SPARC Lab](https://www.ryancosner.com/) with Prof. Ryan Cosner. My work focuses on learned Control Barrier Functions (CBFs) for legged robots — how to make policies that stay safe under disturbances and distribution shift without giving up task performance.

Previously I worked in the [MULIP Lab](https://www.eecs.tufts.edu/~jsinapov/) with Prof. Jivko Sinapov on multi-modal tactile perception and robot skill learning.

**Research interests:** multimodal learning, autonomous systems, robot skill learning, world models (especially JEPA-style approaches).

**Before Tufts:** BS in Computer Science from Brandeis (Magna Cum Laude, May 2024), where I also played NCAA Varsity Baseball. Industry experience at Wealth.com (Software Engineer, backend + security tooling) and HealthFlexx (LLM-based assistant for medical devices, prototyping RAG pipelines).

**In my free time:** basketball, reading philosophy, and practicing MMA.
```

### 3. Drop resume PDF into `files/`

Chris will place `Chris_Liang_Resume.pdf` at `files/Chris_Liang_Resume.pdf`. Confirm the directory exists and the file is referenced correctly by the CV page.

### 4. Set up `_pages/cv.md`

Replace the template CV page with a short intro and a prominent download link. Keep the page minimal — the PDF is the CV.

```markdown
---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
---

{% include base_path %}

My full CV is available as a PDF: [Download CV (PDF)](/files/Chris_Liang_Resume.pdf).

## Education
- **MS in Computer Science**, Tufts University (expected May 2027)
- **BS in Computer Science**, Brandeis University (May 2024, *Magna Cum Laude*)

## Research Experience
- **SPARC Lab, Tufts University** — Graduate Research Assistant (Jan 2026 – Present). Advisor: Prof. Ryan Cosner.
- **MULIP Lab, Tufts University** — Graduate Research Assistant (Aug 2025 – Jan 2026). Advisor: Prof. Jivko Sinapov.

## Professional Experience
- **Wealth.com** — Software Engineer (Jan 2025 – Jul 2025)
- **HealthFlexx** — Applied Scientist Intern (Jun 2023 – Aug 2023)
```

### 5. Create `_pages/research.md`

New page summarizing current research. Add to nav (see task 9).

```markdown
---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
---

## SPARC Lab — Safe + Performant Autonomous Robotics and Control
*Tufts University · Jan 2026 – Present · Advisor: Prof. Ryan Cosner*

At the [SPARC Lab](https://www.ryancosner.com/) we work toward making robots you can trust — robotics research at the intersection of machine learning and control theory, aiming for provably safe and dynamic robot autonomy in real-world settings.

My current work focuses on learned Control Barrier Function (CBF) approaches that navigate the safety-performance tradeoff, adaptively modulating nominal controllers to remain robust under disturbances and distribution shift. I've been architecting and training policy distillation pipelines that produce adaptive safety parameters — bridging data-driven adaptability with formal control-theoretic guarantees, with an eye toward sim-to-real validation on legged robot platforms.

## MULIP Lab — Multi-Modal Learning, Interaction, and Perception
*Tufts University · Aug 2025 – Jan 2026 · Advisor: Prof. Jivko Sinapov*

I worked on multi-modal tactile data collection and transfer learning for robot skill learning. Specifically: building and executing tactile data collection protocols on a UR5 manipulator across a range of tool-use actions, developing pipeline components for data preprocessing and representation analysis, and maintaining broader lab infrastructure.
```

### 6. Create portfolio entries in `_portfolio/`

Remove any template placeholders. Create one markdown file per project below. Use the `_portfolio/portfolio-1.md` naming convention and kebab-case permalinks.

#### `_portfolio/twist-rl.md`
```markdown
---
title: "Twist-RL: Reinforcement Learning for Helical Manipulation"
excerpt: "Extending force-based manipulation learning to helical articulation — training a robot-agnostic policy to unscrew bottle-cap-like objects by learning in object force-space."
collection: portfolio
---

**Course:** Reinforcement Learning, Fall 2025

We extended the FLEX (Force-based Learning for Extended Manipulation) framework to a new class of articulated motion — helical/screw joints — training a robot-agnostic policy that transfers across platforms by learning in object force-space rather than joint configuration space.

**What I built:**
- Designed the MDP: screw-axis state and axial torque action space, multi-term reward combining success, progress, and minimum-torque objectives.
- Constructed a custom helical joint in MuJoCo by coupling hinge and slide joints with an equality constraint.
- Trained a TD3 policy (actor-critic with clipped double Q-learning and delayed actor updates) for continuous control.
- Validated on a Franka arm in Robosuite, producing stable unscrewing behavior on a bottle model.

**Stack:** PyTorch, MuJoCo, Robosuite, Stable Baselines3.
```

#### `_portfolio/trajectory-reconstruction.md`
```markdown
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
```

#### `_portfolio/deep-document-unwarping.md`
```markdown
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
```

#### `_portfolio/brain-hemorrhage-ddpm.md`
```markdown
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
```

#### `_portfolio/legged-robot.md`
```markdown
---
title: "3D-Printed Legged Robot"
excerpt: "Designed, printed, and walked a custom legged robot driven by a Raspberry Pi control stack."
collection: portfolio
---

**Course:** Robotics, Fall 2025

Built a legged robot end-to-end — from CAD design of the mechanical parts through 3D printing, assembly, and the full control stack needed to make it walk.

**What we built:**
- Custom CAD parts for legs, body, and joint brackets.
- Assembly: motors, motor drivers, Raspberry Pi as the control MCU, power conversion electronics.
- Walking gait implementation on the physical platform.

**Stack:** Fusion 360 / CAD tooling, Python on Raspberry Pi.

*Collaborator: (partner led mechanical design).*
```

### 7. Handle template pages we don't want

- `_pages/publications.md`: either delete, OR keep but hide from nav (Chris has no publications yet).
- `_pages/talks.md`: same treatment.
- `_pages/teaching.md`: same treatment.
- `_publications/*.md`: delete all template publication entries.
- `_talks/*.md`: delete all template talks.
- `_teaching/*.md`: delete all template teaching entries.

### 8. Update `_data/navigation.yml`

Top nav should be, in order:

```yaml
main:
  - title: "About"
    url: /
  - title: "CV"
    url: /cv/
  - title: "Research"
    url: /research/
  - title: "Portfolio"
    url: /portfolio/
```

Remove Publications, Talks, Teaching, Blog Posts from nav. (Leave the pages/files themselves in case they're needed later, just unlink from the main menu.)

### 9. Strip or simplify homepage template blocks

The default academicpages `_pages/about.md` has some template sections showing feature blocks, markdown test links, etc. If they're still present after task 2, remove them — keep only the bio content.

### 10. Swap out template images

The default template ships with placeholder images at `images/profile.png` and an image in the site header. If Chris hasn't dropped a real headshot yet:
- Leave `profile.png` as the default (or a plain silhouette) for now.
- Flag to Chris in the final summary that he'll want to replace this.

### 11. Local test

Before committing:

```bash
bundle install
bundle exec jekyll serve
```

Open `http://localhost:4000` and verify:
- Homepage renders the new bio.
- Nav shows About, CV, Research, Portfolio only.
- `/cv/` renders with a working download link to the resume PDF.
- `/research/` renders with both lab entries.
- `/portfolio/` renders all 5 entries.
- No broken links, no leftover template placeholder text ("John Doe", "example.com", etc.).

### 12. Commit and push

Commit message suggestion: `Initial site content: bio, CV, research, portfolio (5 projects)`.

Push to `master` (or whichever branch is configured for GitHub Pages under Settings → Pages). Live site updates within a few minutes.

---

## After Claude Code finishes

Things Chris should manually do later (not this session):
1. Drop a real headshot at `images/profile.png` (square, 400×400px or so works well for academicpages).
2. Update his LinkedIn vanity URL from the ugly default (`xianmai-liang-9b84b5253`) to something clean like `xianmailiang`, then update `_config.yml` to match.
3. Once the site is live, add the actual URL to the resume header (currently uses `chrisliang33.github.io` as a placeholder — verify this is the real deployed URL and swap if different).
4. Add project images / screenshots to each portfolio entry once he has time. Each `_portfolio/*.md` can have a `header.image:` field pointing to an image in `images/`.

---

## Do not

- Do not invent publications, talks, or teaching entries.
- Do not inflate project descriptions with claims not present in this brief.
- Do not add social links beyond GitHub, LinkedIn, and email.
- Do not change the core academicpages layout / theme structure — this is a minimum-viable pass, not a redesign.
