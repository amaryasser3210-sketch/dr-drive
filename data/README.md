# data/ — logged data

**Owner:** Testing and validation. Recorded runs and datasets. Large files are gitignored; keep only small samples.

## Contents
| Path | Purpose |
|---|---|
| `simulation/` | rosbags and metrics from Gazebo runs |
| `hardware/` | rosbags and metrics from real-vehicle runs |

## Conventions
- Name bags: `<task>_<stage>_<YYYYMMDD-HHMM>_<run#>`, e.g. `task2_sim_20261210-1430_r1`.
- Record KPIs (max lateral offset, tape touches, collisions, time) next to each bag.
- Full results tables live in `docs/report/`; raw logs live here.
