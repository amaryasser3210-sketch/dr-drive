# AGENTS.md — Agent Playbook

> Read this first. It tells you what this repo is, what wins when docs disagree, and the rules that
> must not be broken. Keep it short and current.

## What this repo is

`AMR-LNS` (repo `dr-drive`) — the **MCT443s Design of Autonomous Systems** course project: an Autonomous
Mobile Robot that follows a lane and does obstacle avoidance with lane switching, in ROS2/Gazebo and then
on real hardware. **Submission deadline: 25/12/2026.**

**Current maturity: SCAFFOLD-ONLY.** The repo contains the folder structure, documentation, config
templates, and placeholder READMEs. There is **no working code yet** — files described in docs may not
exist. Do not assume a package builds.

## Source of truth / doc conflicts

1. **`HANDBOOK.md` wins** for WBS, ownership, contracts, milestones, schedule.
2. `README.md` is the public landing page and may drift.
3. Folder `README.md` files are **operational only** (how to run, I/O, tuning). Never put theory or
   results there — those live in `docs/report/`.
4. The original assignment: `docs/pdfs/MCT443s_Project_Description_v1.0.pdf`.

## Hard rules

- **SSOT config:** never hardcode parameters, constants, thresholds, or gains. Load from `config/`.
  Load order: `robot_params.yaml → sensor_params.yaml → lane_geometry.yaml → control_gains.yaml`.
- **Do not edit `docs/report/` structure** unless you own Documentation and reporting.
- **Do not make the GitHub repo public** before the submission deadline.
- **No IR line sensors** for lane detection — camera-based only (course rule).
- Keep **shared contracts** (§10 of HANDBOOK) in sync: messages in `amr_interfaces`, the mission FSM
  state enum, lane/obstacle geometry, frame names, and `/cmd_vel` limits.

## Shared contracts to keep in sync

- `amr_interfaces`: `LaneDetection`, `Obstacle`, `ObstacleArray`, `MissionState`.
- Mission FSM states: `IDLE=0, LANE_FOLLOW_RIGHT=1, LANE_FOLLOW_LEFT=2, LANE_CHANGE_LEFT=3, LANE_CHANGE_RIGHT=4, OBSTACLE_STOP=5, FINISHED=6, FAULT=7`.
- Geometry: lane 0.40 m, track 10 m, obstacle 1 right@4 m, obstacle 2 left@8 m, vehicle ≤0.30 m.
- TF frames: `map → odom → base_link → {camera_link, imu_link, lidar_link, left_wheel, right_wheel}`.

## Build / test / lint reality

**No build, test, or lint commands exist yet.** Do not invent them. When packages are implemented, the
intended commands are:

```bash
cd ros2_ws && colcon build --symlink-install && source install/setup.bash
ros2 launch amr_bringup sim.launch.py
```

Update this section the moment real commands exist.

## Git conventions

- Remote: `https://github.com/amaryasser3210-sketch/dr-drive.git`
- Branch model: `main` (protected) ← `dev` ← `feat/<area>-<short>`; `fix/<area>` for hotfixes.
- Commits: Conventional Commits — `feat(perception): ...`, `fix(control): ...`.
- ROS2 software architecture owns merges to `main`. No direct pushes to `main`.
- LF line endings for source; binaries via Git LFS; `build/ install/ log/` are gitignored.

## Directory ownership

Responsibilities are the 8 subsystems from the project description (§2) — see `HANDBOOK.md` §2.2 and §13.

| Folder | Owning responsibility |
|---|---|
| `config/` | all |
| `ros2_ws/src/amr_description`, `amr_simulation`, `modeling/` | Robot modeling and simulation |
| `ros2_ws/src/*` (architecture, `amr_bringup`, `amr_interfaces`) | ROS2 software architecture |
| `ros2_ws/src/amr_perception` | Perception and sensing |
| `ros2_ws/src/amr_localization` | State estimation |
| `ros2_ws/src/amr_control` | Control system design |
| `hardware/`, `firmware/`, `ros2_ws/src/amr_hardware` | Hardware integration |
| `data/`, `docs/logs/` | Testing and validation |
| `docs/report/` | Documentation and reporting |
