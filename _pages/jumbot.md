---
layout: single
title: "Jumbot-B: A 3D-Printed Bipedal Robot"
permalink: /jumbot/
author_profile: true
toc: true
toc_label: "Contents"
toc_sticky: true
---

**Team:** Xianmai (Chris) Liang · Zhenkai Gao
**Course:** ME 143 — Spring 2026, Tufts University

A 3D-printed bipedal robot built end-to-end: CAD, fabrication, electronics, and gait tuning. Jumbot-B walks at a best speed of **4 cm/sec** using manually-tuned periodic gaits derived from servo encoder data.

[**Demo videos (Google Drive) →**](https://drive.google.com/drive/folders/1ROvHOyrOt20AlWEoPkbIN6lXl_CtkAe5?usp=sharing)

> *Working portfolio — sections marked __coming__ are in progress.*

---

## Overview

Jumbot-B is a small bipedal robot driven by six servos and a Raspberry Pi, with chassis and feet 3D-printed in PLA. Each leg has hip yaw + hip roll, knee, and ankle joints — enough articulation to shift weight and twist the body during single-support phases of a gait.

We tuned gaits directly on the hardware using servo encoder feedback rather than running a simulation track.

## Robot Design & CAD

> CAD renders and design rationale — **coming**.

Key design choices:

- **DOFs (per leg):** hip yaw + hip roll, knee, ankle.
- **Materials:** PLA for the chassis and feet — rigid, predictable contact dynamics.
- **Sensing:** servo encoders provide joint state feedback used for gait tuning.
- **Compute:** Raspberry Pi runs the gait controller and commands the servos.

## Mechanical Assembly

> Build photos and iteration shots — **coming**.

Notable changes across revisions:

- **TPU foot experiment.** We replaced PLA feet with TPU (85A) hoping for better ground compliance. The flexibility expanded the gait search problem — the robot lost static balance and was harder to control — and we reverted to PLA.
- **Power delivery upgrade.** The original thin wiring between the DC converter and battery produced enough voltage drop to make servo behavior inconsistent. Replacing it with thicker-gauge cables stabilized the power rail and the gait reliability immediately improved.

## Hardware Implementation

> Walking video — **coming**.

The robot is controlled by a Raspberry Pi running a periodic gait function. Servo commands go out over GPIO; encoder positions are read back to record waypoints during tuning.

## Baseline Performance

| Metric | Value |
|---|---|
| Best forward speed | **4 cm/sec** |
| Gait approach | Manual periodic function from encoder waypoints |
| DOFs (per leg) | hip yaw + hip roll + knee + ankle |

> Iteration-by-iteration baseline table — **coming**.

## Gait Development

Our approach to gait generation:

1. Manually pose the robot through one walking cycle, capturing joint angles at each transitional state via the servo encoders.
2. Use those waypoints to construct a periodic function for the joint trajectories.
3. Iterate by hand, adjusting timing and amplitude until the robot walks stably.

The hip yaw + roll axes give Jumbot-B more body-twisting capability — useful for shifting the center of mass during single-support phases — but they also widen the gait search space, which is the main reason gait tuning has been the slow part of the project. Once roughly half a walking cycle is dialed in, the other half tends to mirror it.

## Learning Curve

> Best speed vs. iteration plot — **coming**.

## Motor Data

> Motor speed / position / torque plots — **coming**.

## Other Goals & Environments

> Turning, uneven terrain, obstacles — **coming**.

## Final Optimized Gait

> Final-gait video with performance metrics overlay — **coming**.

In the meantime, full build and test footage lives in the [Drive folder](https://drive.google.com/drive/folders/1ROvHOyrOt20AlWEoPkbIN6lXl_CtkAe5?usp=sharing).

## Results & Comparison

> Summary table comparing iterations — **coming**.

## Energy Efficiency

> Power draw / energy-per-meter analysis — **coming**.

## Lessons Learned

- **Material choice has hidden second-order effects.** TPU feet looked good on paper for compliance, but the flexibility blew up the gait problem and broke static balance.
- **Power delivery is invisible until it isn't.** Thin wires produced enough voltage drop to make servo behavior inconsistent — symptoms looked like control bugs but were really hardware. Thick cables fixed it.
- **Sim-to-real has a fixed setup cost.** When that cost is high relative to the iteration budget — as it was once Onshape URDF export proved unreliable — tuning directly on hardware can dominate.
- **Encoder-driven manual gaits work.** The waypoint-based periodic function is crude but converges quickly once you find the first half of the cycle.

## Future Work

- Refine the walking gait beyond the current 4 cm/sec.
- Land the Onshape → URDF pipeline so we can prototype gaits in MuJoCo before committing to hardware.
- Add new locomotion modes: turning, uneven terrain, jumping.
- Energy efficiency analysis: current draw vs. velocity, energy per meter.

## Code Repository

> Code repo link — **coming**.

## Acknowledgements

Built for **ME 143 — Spring 2026** at Tufts University. Thanks to the course staff for the platform and feedback throughout the term.

Project by Xianmai (Chris) Liang and Zhenkai Gao.
