# amr_hardware

**Owner:** Hardware integration. ROS2 drivers for the physical vehicle.

## Nodes
| Node | Role |
|---|---|
| `wheel_encoder_driver` | reads encoders → `/joint_states` |
| `motor_driver` | `/cmd_vel` → motor PWM (serial/CAN to MCU) |
| `camera_driver` | camera → `/camera/image_raw` |
| `imu_driver` | IMU → `/imu/data` |
| `range_driver` | LiDAR/ultrasonic → `/scan` or `/range` |

## Interface
- `/cmd_vel` (`geometry_msgs/Twist`) in, following the clamps in `config/robot_params.yaml`.
- Wireless only if using external processing (Arduino/ESP32 + laptop) — **no cables**.

## Related
- Embedded firmware: `../../firmware/`
- Electronics/schematics: `../../hardware/electronics/`
