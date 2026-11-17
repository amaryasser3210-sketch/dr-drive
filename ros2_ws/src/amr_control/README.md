# amr_control

**Owner:** Control system design. Motion control and mission logic.

## Nodes
| Node | Subscribes | Publishes |
|---|---|---|
| `motion_controller_node` | `/perception/lane`, `/perception/obstacles`, `/state_estimate`, `/mission/state` | `/cmd_vel` |
| `mission_fsm_node` | `/perception/*`, `/state_estimate` | `/mission/state` |

## Controllers
- Lateral: **Stanley** or **Pure Pursuit** (selected in `config/control_gains.yaml`).
- Longitudinal: **speed PID**.
- Lane change: right→left and left→right manoeuvres, sensor-triggered.

## Mission FSM states
`IDLE=0, LANE_FOLLOW_RIGHT=1, LANE_FOLLOW_LEFT=2, LANE_CHANGE_LEFT=3, LANE_CHANGE_RIGHT=4, OBSTACLE_STOP=5, FINISHED=6, FAULT=7` (contract — `HANDBOOK.md` §10.2).

## Tuning
All gains in `config/control_gains.yaml`. Never hardcode.
