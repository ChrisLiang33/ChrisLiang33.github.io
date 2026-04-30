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
**Course:** ME 134 — Robotics Studio, Spring 2026, Tufts University

A 3D-printed bipedal robot built end-to-end: CAD, fabrication, electronics, and gait tuning. Jumbot-B walks at a best speed of **4 cm/sec** using manually-tuned periodic gaits derived from servo encoder data.

[**Walking video →**](https://drive.google.com/file/d/147QfC2F2BtMzXfndmTY_-xQ9kmrhRBI7/view?usp=sharing) · [**All build & test footage (Drive folder) →**](https://drive.google.com/drive/folders/1ROvHOyrOt20AlWEoPkbIN6lXl_CtkAe5?usp=sharing)

> *Working portfolio — sections marked __coming__ are in progress.*

---

## Overview

Jumbot-B is a small bipedal robot driven by eight servos and a Raspberry Pi, with chassis and feet 3D-printed in PLA. Each leg has hip pitch + hip yaw + hip roll plus a knee/leg joint — enough articulation to shift weight and twist the body during single-support phases of a gait.

We tuned gaits directly on the hardware using servo encoder feedback rather than running a simulation track.

### Robot Specifications

| Spec | Value |
|---|---|
| Total weight | 15 lb |
| Walking speed (sustained max) | 0.5 in/sec (~1.27 cm/sec) |
| Walking speed (best) | **4 cm/sec** |
| Walking terrain | Flat surface |
| Peak power draw | 9 V · 0.6 A · **5.4 W** |
| Compute | Raspberry Pi |
| Drive | 8 servos with position/velocity/temperature/voltage feedback |
| Material | PLA for most body parts |

## Robot Design & CAD

> CAD render — **coming** *(drop the white render from the title slide at `images/jumbot/glamour.png`)*.

Key design choices:

- **DOFs (per leg):** hip pitch + hip yaw + hip roll + knee/leg.
- **Materials:** PLA for the chassis and feet — rigid, predictable contact dynamics.
- **Sensing:** each servo reports position, velocity, temperature, and bus voltage; encoder data drives the gait tuning loop.
- **Compute:** a Raspberry Pi runs the gait controller and commands the servos directly over GPIO.

## Mechanical Assembly

> Build / iteration photos — **coming** *(drop iteration shots and the walking-frame sequence in `images/jumbot/`)*.

Notable changes across revisions:

- **TPU foot experiment.** We replaced PLA feet with TPU (85A) hoping for better ground compliance. The flexibility expanded the gait search problem — the robot lost static balance and was harder to control — and we reverted to PLA.
- **Power delivery upgrade.** The original thin wiring between the DC converter and battery produced enough voltage drop to make servo behavior inconsistent. Replacing it with thicker-gauge cables stabilized the power rail and gait reliability immediately improved.
- **Cable routing.** Wiring tidied and bundled along the chassis so legs can swing without snagging.

## Hardware Implementation

The robot is controlled by a Raspberry Pi running a periodic gait function. Servo commands go out directly over GPIO; encoder positions are read back to record waypoints during tuning. Power comes from an onboard battery via a DC converter.

**Walking video:** [Jumbot-B taking baby steps](https://drive.google.com/file/d/147QfC2F2BtMzXfndmTY_-xQ9kmrhRBI7/view?usp=sharing)

> Walking-frame sequence still — **coming** *(drop at `images/jumbot/walking-frames.jpg`)*.

## Performance & Learning Curve

Speed measurements across iterations:

| Iteration | Speed (in/sec) | Speed (cm/sec) | Notes |
|---|---|---|---|
| Baby Steps — sustained max | 0.5 | 1.27 | First reliable walking gait |
| Baby Steps — fastest single cycle | 1.0 | 2.54 | 2 in/cycle, 2 sec/cycle |
| Final Performance | ~1.6 | **4.0** | After power-rail upgrade and gait re-tuning |

That's roughly a **3.1× speedup** from first walking gait to final, driven by hardware reliability fixes (thicker power wiring, cable management) and additional gait waypoint tuning.

> Plot of best speed vs. iteration — **coming** *(generate from the table above as `images/jumbot/learning-curve.png`)*.

## Gait Development

Our approach to gait generation:

1. Manually pose the robot through one walking cycle, capturing joint angles at each transitional state via the servo encoders.
2. Use those waypoints to construct a periodic function for the joint trajectories.
3. Iterate by hand, adjusting timing and amplitude until the robot walks stably.

The hip yaw + roll axes give Jumbot-B more body-twisting capability — useful for shifting the center of mass during single-support phases — but they also widen the gait search space, which is the main reason gait tuning has been the slow part of the project. Once roughly half a walking cycle is dialed in, the other half tends to mirror it.

## Motor Data

We log per-servo position, velocity, temperature, and bus voltage during a walking cycle. The figure below covers an 8-second window across all 8 servos (Hip Pitch 1/2, Hip Yaw 1/2, Hip Roll 1/2, Leg 1/2):

- **Position (deg):** sinusoidal trajectories with leg/hip-pitch joints traversing the largest range; the periodic structure is exactly what the gait function commands.
- **Velocity (deg/s):** derivative of position; peaks near ±90 deg/s for the swing-leg joints.
- **Temperature (°C):** servos warm steadily from ~30 °C to ~40 °C over the run — comfortably below the failure window.
- **Bus voltage (mV):** ~8400–8800 mV with the upgraded wiring; pre-upgrade dips that caused jitter are no longer present.

> Servo data plot — **coming** *(drop at `images/jumbot/servo-data.png`)*.

## Robot Reliability Routines

- **Health check on boot:** queries each servo for position, temperature, and voltage; aborts startup if any servo fails to respond or reports out-of-range temperature.
- **Shutdown routine:** detorques servos, returns to a safe pose, then powers down — prevents the robot from collapsing under its own weight when killed mid-run.

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

[github.com/ChrisLiang33/jumbotB](https://github.com/ChrisLiang33/jumbotB)

## Citations

[1] Sun, B., Mohamed Haris, S., & Ramli, R. (2026). A Systematic Review of Deep Reinforcement Learning for Legged Robot Locomotion. *Instruments*, 10(1), 8. <https://www.mdpi.com/2410-390X/10/1/8>

## Acknowledgements

Built for **ME 134 — Robotics Studio, Spring 2026** at Tufts University. Thanks to the course staff for the platform and feedback throughout the term.

Project by Xianmai (Chris) Liang and Zhenkai Gao.
