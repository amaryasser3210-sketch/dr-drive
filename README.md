# AMR‑LNS — Autonomous Mobile Robot · Lane Navigation System

> MCT443s **Design of Autonomous Systems** — Course Project.
> Design, simulate, and implement an Autonomous Mobile Robot (AMR) that follows a lane and
> avoids obstacles with lane switching, first in **ROS2/Gazebo**, then on a **built ground vehicle**.

**Submission deadline: 25 / 12 / 2026.**

---

## What this repo is

A team project (7–8 students) split across 8 subsystems:

1. Robot modeling & simulation
2. ROS2 software architecture
3. Perception & sensing
4. State estimation
5. Control system design
6. Hardware integration
7. Testing & validation
8. Documentation & reporting

**The operational truth lives in [`HANDBOOK.md`](HANDBOOK.md)** — WBS, ownership matrix, shared
contracts, milestones, and the weekly plan. When `README.md` and the handbook disagree, **the handbook wins.**

---

## The two tasks

- **Task 1 — Lane following:** stay on the center of a straight 40 cm × 10 m lane, hold heading, control speed. Camera + IMU required.
- **Task 2 — Obstacle avoidance with lane switching:** two-lane track; start right lane; obstacle 1 (right, 4 m) → switch left; obstacle 2 (left, 8 m) → switch right; finish. Camera-based lane detection only (no IR line sensors).

---

## Quick start (planned — not yet implemented)

> ⚠️ Scaffold-only: this repo currently contains **structure and documentation**, not working code.
> Commands below are the intended workflow and will be real once packages are implemented.

```bash
# 1. Build the ROS2 workspace
cd ros2_ws
colcon build --symlink-install
source install/setup.bash

# 2. Launch the simulation (Gazebo + all nodes)
ros2 launch amr_bringup sim.launch.py

# 3. Launch on the real vehicle
ros2 launch amr_bringup hardware.launch.py
```

---

## Repository layout

```
config/        SSOT: robot params, sensors, lane geometry, control gains
ros2_ws/src/   ROS2 packages (description, simulation, perception, localization,
               control, hardware, interfaces, bringup)
modeling/      mathematical modeling + optional MATLAB/Simulink (bonus)
firmware/      embedded code for the microcontroller
hardware/      CAD, electronics, BOM
gui/           teleop / dashboard / visualizer
data/          rosbags from simulation and hardware runs
docs/          report, logs, reference PDFs, resources
scripts/       utility scripts (build, run, record)
```

See [`HANDBOOK.md`](HANDBOOK.md) §9 for the full architecture and node graph.

---

## Rules of the road

- **No hardcoded constants** — everything loads from `config/`.
- **Folder READMEs are operational only**; theory and results live in `docs/report/`.
- **Don't invent build/test commands** — if a command isn't documented here or in a package README, it doesn't exist yet.
- The GitHub repo stays **private until the submission deadline**, then **public at submission**.
