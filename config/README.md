# config/ — Single Source of Truth (SSOT)

**Every parameter, constant, threshold, and gain lives here. Nothing is hardcoded elsewhere.**

## Load order

```
1. robot_params.yaml    (physical robot)
2. sensor_params.yaml   (sensors)
3. lane_geometry.yaml   (environment / track)
4. control_gains.yaml   (controllers)
```

Nodes must read these files (ROS2 `params` files or an explicit loader). If a value is needed by more
than one node, it belongs here — not duplicated in code.

## Files

| File | Owns |
|---|---|
| `robot_params.yaml` | wheelbase, wheel radius, mass, speed limits, encoder resolution |
| `sensor_params.yaml` | camera, IMU, LiDAR/ultrasonic specs and mounting |
| `lane_geometry.yaml` | lane width, track length, obstacle positions, tape thresholds |
| `control_gains.yaml` | PID gains, Pure Pursuit / Stanley parameters, lane-change tuning |

> Values below are **placeholders** to be confirmed by the responsible subsystem. Do not treat them as
> measured. Update the file, not a hardcoded copy.
