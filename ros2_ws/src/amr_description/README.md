# amr_description

**Owner:** Robot modeling and simulation. Robot model: URDF/xacro, meshes, RViz config.

## Contents
- `urdf/` — xacro robot description (differential drive)
- `meshes/` — visual meshes (LFS)
- `rviz/` — RViz display configs

## Notes
- Frames must match the TF contract: `map → odom → base_link → {camera_link, imu_link, lidar_link, left_wheel, right_wheel}`.
- Dimensions come from `config/robot_params.yaml` — do not hardcode.
