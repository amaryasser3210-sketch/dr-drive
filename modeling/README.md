# modeling/ — mathematical modeling

**Owner:** Robot modeling and simulation. Mathematical models of the vehicle and (optionally) the full task.

## Contents
| Path | Purpose |
|---|---|
| `derivations/` | kinematic/dynamic derivations, state-space, motion equations |
| `matlab/` | optional MATLAB/Simulink models (bonus, description §5.7) |

## Anti-drift rule
Formal derivations and results are centralized in `docs/report/`. This folder holds the **working**
models/scripts; the report holds the write-up.

## Interfaces
Physical parameters come from `config/robot_params.yaml` (SSOT) — never hardcode.
