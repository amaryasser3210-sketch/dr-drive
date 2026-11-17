# amr_interfaces

**Owner:** ROS2 software architecture. Custom ROS2 messages shared across all packages.

## Messages (contract — see `HANDBOOK.md` §10.1)

- `LaneDetection.msg` — lateral offset, heading error, curvature, confidence
- `Obstacle.msg` — range, bearing, lane, distance from start, confidence
- `ObstacleArray.msg` — header + `Obstacle[]`
- `MissionState.msg` — FSM state + description

**Changing a message requires notifying every owner** (integration contract).
