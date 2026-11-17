# amr_bringup

**Owner:** ROS2 software architecture. Top-level launch and node composition.

## Launch files (planned)
- `sim.launch.py` — Gazebo world + robot spawn + all perception/localization/control nodes
- `hardware.launch.py` — real drivers + all nodes
- `task1.launch.py`, `task2.launch.py` — task-specific worlds/config

## Usage
```bash
ros2 launch amr_bringup sim.launch.py
ros2 launch amr_bringup hardware.launch.py
```

Sim vs real differences are parameterized (via `config/`), not forked code.
