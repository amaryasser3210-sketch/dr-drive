# scripts/ — utility scripts

**Owner:** ROS2 software architecture. Helper scripts for building, running, and recording.

Planned scripts:
- `build.sh` — `colcon build --symlink-install` from `ros2_ws/`
- `run_sim.sh` — launch the simulation
- `run_hardware.sh` — launch on the real vehicle
- `record.sh` — record a rosbag for a task
- `metrics.sh` — extract KPIs (lateral offset, tape touches, time) from a bag

Keep scripts thin wrappers; do not duplicate node logic.
