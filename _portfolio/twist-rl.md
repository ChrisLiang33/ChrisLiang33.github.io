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
