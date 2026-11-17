# firmware/src/

Firmware source files.

Typical responsibilities:
- read wheel encoders (interrupts/quadrature)
- drive motor drivers via PWM
- read IMU / ultrasonic if attached to the MCU
- speak the serial/wireless protocol (see `../protocol/`)
