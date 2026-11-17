# amr_localization

**Owner:** State estimation. Localization and sensor fusion.

## Approach
Wheel odometry + EKF fusion of **IMU + wheel encoders** (via `robot_localization` or a custom EKF).
Satisfies description §5.4 (at least one of odometry / fusion / basic pose estimation).

## Node
| Node | Subscribes | Publishes |
|---|---|---|
| `localization_node` | `/joint_states`, `/imu/data` | `/odom`, `/state_estimate`, TF |

## I/O definitions
- Publishes the TF chain `odom → base_link`.
- `/state_estimate` carries pose + heading used by control and the mission FSM.

## Tuning
Noise covariances and IMU bias handling documented in `docs/report/` (state-estimation section).
