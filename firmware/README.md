# firmware/ — embedded code

**Owner:** Hardware integration. Code for the microcontroller (e.g. ESP32/Arduino/Teensy) that drives motors and reads
sensors at the low level.

## Contents
| Path | Purpose |
|---|---|
| `src/` | firmware source |
| `include/` | headers |
| `protocol/` | serial/wireless protocol between MCU and the ROS2 host |

## Protocol contract
Document the command/telemetry packet format in `protocol/` and keep it in sync with
`ros2_ws/src/amr_hardware` (motor driver / encoder driver).

## Notes
- Build with PlatformIO or the Arduino/ESP-IDF toolchain (record the exact command here once it exists).
- Wireless only if using external processing — no cables during runs.
