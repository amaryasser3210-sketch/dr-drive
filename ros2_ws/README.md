# ros2_ws/ — ROS2 workspace

The ROS2 (colcon) workspace for AMR‑LNS. All robot software lives under `src/`.

## Packages

| Package | Owner | Purpose |
|---|---|---|
| `amr_interfaces` | ROS2 software architecture | Custom messages: `LaneDetection`, `Obstacle`, `ObstacleArray`, `MissionState` |
| `amr_description` | Robot modeling and simulation | URDF/xacro robot model, meshes, RViz config |
| `amr_simulation` | Robot modeling and simulation | Gazebo worlds (straight lane, two-lane) + simulation launch |
| `amr_perception` | Perception and sensing | Camera lane detection, obstacle detection |
| `amr_localization` | State estimation | Wheel odometry + EKF (IMU + encoders) |
| `amr_control` | Control system design | Lateral controller, speed PID, mission FSM |
| `amr_hardware` | Hardware integration | Hardware drivers (motors, encoders, camera, IMU, LiDAR) |
| `amr_bringup` | ROS2 software architecture | Top-level launch files and node composition |

## Build

```bash
cd ros2_ws
colcon build --symlink-install
source install/setup.bash
```

> Not yet implemented — packages do not exist as working code. This is the intended workflow.

See `HANDBOOK.md` §9 for the node graph and `§10` for the shared contracts.
