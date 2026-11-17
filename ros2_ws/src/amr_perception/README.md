# amr_perception

**Owner:** Perception and sensing. Lane detection and obstacle detection.

## Nodes
| Node | Subscribes | Publishes |
|---|---|---|
| `lane_detection_node` | `/camera/image_raw` | `/perception/lane` (`LaneDetection`) |
| `obstacle_detection_node` | `/scan` or `/range` | `/perception/obstacles` (`ObstacleArray`) |

## I/O definitions
- `LaneDetection`: `lateral_offset` (m, +right), `heading_error` (rad), `curvature`, `confidence`.
- `Obstacle`: `range` (m), `bearing` (rad, +left), `lane` (0/1/2), `distance_from_start`, `confidence`.

## Tuning
Lane thresholds live in `config/lane_geometry.yaml`. Camera-based lane detection only —
**IR line sensors are prohibited**.

## Notes
- Lane detection must run on the straight lane (Task 1) and support lane classification (Task 2).
- Log detection reliability to `docs/logs/`.
