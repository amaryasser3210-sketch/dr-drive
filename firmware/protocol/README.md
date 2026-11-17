# firmware/protocol/

Serial/wireless protocol between the microcontroller and the ROS2 host.

Define here:
- frame format (header, payload, checksum)
- command messages (set velocity, stop, e-stop)
- telemetry messages (encoder counts, status)

This is a **shared contract** — keep it in sync with `ros2_ws/src/amr_hardware`.
