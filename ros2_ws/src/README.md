# src/ — ROS2 packages

One folder per package. See `../README.md` for the package table.

Create a package with:

```bash
ros2 pkg create --build-type ament_python <name> --dependencies rclpy
ros2 pkg create --build-type ament_cmake <name> --dependencies rclcpp
```

Keep parameters in `config/` at the repo root (SSOT) — do **not** hardcode them in nodes.
