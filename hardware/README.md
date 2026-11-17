# hardware/ — physical artifacts

**Owner:** Hardware integration. Everything about the physical vehicle.

## Contents
| Path | Purpose |
|---|---|
| `cad/` | chassis CAD, STEP, meshes |
| `electronics/` | schematics, wiring, pinouts |
| `bom/` | bill of materials, procurement status |

## Spec constraints (description §3.1)
- max width **30 cm** (fits a 40 cm lane)
- two DC motors, rear-wheel drive
- steering by servo **or** differential drive

Embedded firmware lives in `../firmware/`; ROS2 drivers in `../ros2_ws/src/amr_hardware`.
