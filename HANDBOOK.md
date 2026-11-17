# HANDBOOK.md — Master Operational Spec

> **This is the single source of truth (SSOT) for *how the project is run*.**
> It owns the WBS, ownership matrix, shared contracts, milestones, and the weekly plan.
> `README.md` is the public landing page and **may drift**; when the two disagree, **this file wins**.

---

## 1. Project Identity

| Field | Value |
|---|---|
| Course | MCT443s — Design of Autonomous Systems |
| Deliverable | Course Project (v1.0 description) |
| Project codename / abbreviation | **AMR‑LNS** — *Autonomous Mobile Robot — Lane Navigation System* |
| Full title | Design, Simulation and Implementation of an Autonomous Mobile Robot for Structured Lane Navigation |
| Team size | 7–8 students |
| Stages | (1) Simulation in ROS2 → (2) Hardware deployment |
| Submission deadline | **25 / 12 / 2026** (Week 15) |
| Repository | `https://github.com/amaryasser3210-sketch/dr-drive` — private until submission deadline, **public at submission** |
| Description source | `docs/pdfs/MCT443s_Project_Description_v1.0.pdf` |

### 1.1 Why the codename
The description has no short name. `AMR‑LNS` is used only as an internal handle for the report and file
naming. It is **not** part of the graded deliverable — the report title stays the formal one above.

---

## 2. Abbreviations & Glossary

Abbreviations taken from, and used to read, the project description.

| Abbrev. | Meaning |
|---|---|
| **AMR** | Autonomous Mobile Robot |
| **ROS2** | Robot Operating System 2 (middleware; nodes over topics/services/actions) |
| **Gazebo** | Physics simulator used for the simulation stage |
| **CV** | Computer Vision |
| **IMU** | Inertial Measurement Unit (accel + gyro) |
| **LiDAR** | Light Detection and Ranging (laser range sensor) |
| **DC** | Direct Current (drive motors) |
| **PWM** | Pulse Width Modulation (motor speed control) |
| **PID** | Proportional–Integral–Derivative controller |
| **EKF** | Extended Kalman Filter (sensor fusion) |
| **FSM** | Finite State Machine (supervisory / mission logic) |
| **ROI** | Region Of Interest (image crop for CV) |
| **HSV** | Hue–Saturation–Value colour space (image thresholding) |
| **TF** | ROS2 Transform tree (coordinate frames) |
| **cmd_vel** | ROS2 standard velocity command topic (`geometry_msgs/Twist`) |
| **odom** | Odometry (pose/speed estimated from wheel encoders) |
| **bag / rosbag** | Recorded ROS2 message log |
| **URDF** | Unified Robot Description Format (robot model) |
| **SSOT** | Single Source Of Truth |
| **WBS** | Work Breakdown Structure |
| **KPI** | Key Performance Indicator |
| **DoD** | Definition of Done |
| **HW / SW** | Hardware / Software |
| **IR** | Infrared (line sensors — **prohibited** for lane detection) |

### 2.2 Project responsibilities (from description §2)

1. Robot modeling and simulation
2. ROS2 software architecture
3. Perception and sensing
4. State estimation
5. Control system design
6. Hardware integration
7. Testing and validation
8. Documentation and reporting

---

## 3. Project Overview (from description §1)

Design, simulate, and implement an **AMR** performing structured navigation tasks in a controlled
environment. The system covers: mathematical modeling, simulation & algorithm development, sensor
integration, control implementation, and real-world hardware testing.

**Stage 1 — Simulation:** full system developed and tested in **ROS2** (MATLAB/Simulink optional, bonus).
**Stage 2 — Hardware:** deployed on a small autonomous ground vehicle built by the team.

MATLAB/Simulink implementation is **optional** and earns **bonus marks** (see §11.4).

---

## 4. Vehicle Platform Spec (from description §3)

### 4.1 Mechanical (§3.1)
- Must fit a **40 cm lane** → **max width 30 cm**.
- **Two DC motors** for **rear-wheel drive**.
- Steering by a **servo motor** *or* by **differential drive**.

### 4.2 Processing unit (§3.2) — any one of
- Raspberry Pi, **or** NVIDIA Jetson Nano, **or**
- Arduino/ESP32 + external processing (laptop) with **wireless** connectivity (no cables), **or**
- an equivalent embedded computer.

### 4.3 Sensors (§3.3) — **minimum, all required and must be used**

| Sensor | Purpose |
|---|---|
| Camera | Lane detection |
| IMU | Orientation estimation |
| Ultrasonic **or** LiDAR | Obstacle detection |
| Wheel encoders | Odometry and speed measurement |

> Additional sensors (e.g. proximity) are allowed.

---

## 5. Task Definitions (from description §4)

### 5.1 Task 1 — Lane Following (§4.1)
Straight single-lane road, **40 cm wide, 10 m long**. Follow the **lane center**, maintain **heading**,
complete the path **without leaving the lane**. Must implement lane detection, lateral control, heading
stabilization, and speed control, using **at least camera + IMU**.

### 5.2 Task 2 — Obstacle Avoidance with Lane Switching (§4.2)
Straight **two-lane** road (40 cm each, 10 m). Two obstacles at **fixed positions**:

| Obstacle | Lane | Distance from start |
|---|---|---|
| 1 | Right | 4 m |
| 2 | Left | 8 m |

Sequence: start in **right lane** → detect obstacle 1 → switch to **left lane** → detect obstacle 2 →
switch back to **right lane** → finish. Stay within lane boundaries, avoid collisions, minimize time.

**Rules:** lane changes must be **triggered by sensor detection** (algorithm reviewed in the discussion,
§8). **IR line-following sensors are NOT allowed.** Lanes are **black electrical tape**; lane detection
**must be camera-based**. Obstacles may be bags or cardboard boxes.

---

## 6. Simulation Requirements (from description §5)

| § | Requirement | Owner (responsibility) |
|---|---|---|
| 5.1 | Robot modeling: kinematics (diff-drive or bicycle), motion equations | Robot modeling and simulation |
| 5.2 | Sensor simulation: camera lane detection, obstacle detection, IMU | Perception and sensing |
| 5.3 | Perception: CV lane detection, obstacle detection, environment representation | Perception and sensing |
| 5.4 | Localization: ≥1 of odometry / IMU+odometry fusion / basic pose estimation | State estimation |
| 5.5 | Motion control: PID, Pure Pursuit, or Stanley — lane-center, smooth lane change, stable heading | Control system design |
| 5.6 | ROS2 architecture: nodes over topics (lane det., obstacle det., localization, motion controller, robot driver); must demonstrate communication | ROS2 software architecture |
| 5.7 | MATLAB/Simulink (optional, bonus) | Robot modeling and simulation |

---

## 7. Hardware Implementation (from description §6)
After successful simulation, move the system to the physical vehicle: motor drivers, required sensors,
embedded computer, and a **ROS2 interface**. The vehicle must complete **both tasks** in a real test
environment.

---

## 8. Deliverables (from description §9)

| # | Deliverable | Contents | Primary owner (responsibility) |
|---|---|---|---|
| 9.1 | **Technical Report** | robot design, system architecture, math modeling, simulation methodology, perception algorithms, state estimation, control design, ROS2 implementation, experimental results, performance analysis, discussion & conclusions | Documentation and reporting (+ all) |
| 9.2 | **Code & simulation files** | ROS2 packages (worlds + launch files); MATLAB/Simulink if optional attempted; **organized folder structure with README**; **public GitHub link** in report | ROS2 software architecture (+ all) |
| 9.3 | **Project Video (5–10 min)** | robot, simulation, ROS2 architecture, hardware, execution of both tasks, observations & conclusions | Documentation and reporting |
| 9.4 | **Team Responsibility Sheet** | each member's responsibilities, subsystem contributions, coding & implementation tasks | Documentation and reporting |

---

## 9. System Architecture

### 9.1 Domain → repository mapping (BPS-style)

| Domain | Folder | Responsibility |
|---|---|---|
| SSOT parameters | `config/` | all |
| Robot model & sim | `ros2_ws/src/amr_description`, `amr_simulation` | Robot modeling and simulation |
| ROS2 software | `ros2_ws/src/*` (all packages) | ROS2 software architecture |
| Perception & sensing | `ros2_ws/src/amr_perception` | Perception and sensing |
| State estimation | `ros2_ws/src/amr_localization` | State estimation |
| Control | `ros2_ws/src/amr_control` | Control system design |
| Hardware & firmware | `hardware/`, `firmware/`, `ros2_ws/src/amr_hardware` | Hardware integration |
| Testing & data | `data/`, `docs/logs/` | Testing and validation |
| Docs & report | `docs/report/`, `docs/` | Documentation and reporting |
| Math modeling (incl. MATLAB bonus) | `modeling/` | Robot modeling and simulation |
| Utilities | `scripts/`, `gui/` | ROS2 software architecture / Hardware integration |

### 9.2 ROS2 node graph (target)

```
 [camera_driver] --/camera/image_raw--> [lane_detection_node] --/perception/lane------+
 [imu_driver]    --/imu/data---------> [localization_node]    --/state_estimate-----+--> [motion_controller_node] --/cmd_vel--> [robot_driver]
 [lidar/ultra]   --/scan or /range---> [obstacle_detection]   --/perception/obstacles-+                                          (sim: Gazebo plugin
 [encoders]      --/joint_states-----> [localization_node]    --/odom----------------+                                            hw: serial motor ctrl)
                                                                                          ^
                                                                       [mission_fsm_node] --/mission/state
```

### 9.3 Nodes

| Node | Package | Subscribes | Publishes |
|---|---|---|---|
| `camera_driver` | amr_hardware / sim | — | `/camera/image_raw`, `/camera/camera_info` |
| `imu_driver` | amr_hardware / sim | — | `/imu/data` |
| `range_driver` | amr_hardware / sim | — | `/scan` (LiDAR) or `/range` (ultrasonic) |
| `wheel_encoder_driver` | amr_hardware / sim | — | `/joint_states` |
| `lane_detection_node` | amr_perception | `/camera/image_raw` | `/perception/lane` |
| `obstacle_detection_node` | amr_perception | `/scan` or `/range` | `/perception/obstacles` |
| `localization_node` | amr_localization | `/joint_states`, `/imu/data` | `/odom`, `/state_estimate`, TF |
| `mission_fsm_node` | amr_control | `/perception/*`, `/state_estimate` | `/mission/state` |
| `motion_controller_node` | amr_control | `/perception/lane`, `/perception/obstacles`, `/state_estimate`, `/mission/state` | `/cmd_vel` |
| `robot_driver` | amr_hardware / sim | `/cmd_vel` | `/joint_states` (sim) / serial (hw) |

---

## 10. Shared Contracts (must stay in sync across all subsystems)

> Changing anything in this section requires notifying **every** owner. These are the integration points.

### 10.1 Custom messages (`amr_interfaces`)

```
# LaneDetection.msg
std_msgs/Header header
float32 lateral_offset   # m, +right / -left, vehicle center vs lane center
float32 heading_error    # rad, lane tangent vs vehicle heading
float32 curvature        # 1/m
float32 confidence       # 0..1

# Obstacle.msg
float32 range            # m
float32 bearing          # rad, +left / -right
uint8   lane             # 0=unknown 1=left 2=right
float32 distance_from_start
float32 confidence

# ObstacleArray.msg
std_msgs/Header header
Obstacle[] obstacles

# MissionState.msg
std_msgs/Header header
uint8  state
string description
```

### 10.2 Mission FSM state enum (`mission_fsm_node`)

| Value | Name | Meaning |
|---|---|---|
| 0 | `IDLE` | waiting / start |
| 1 | `LANE_FOLLOW_RIGHT` | following right lane |
| 2 | `LANE_FOLLOW_LEFT` | following left lane |
| 3 | `LANE_CHANGE_LEFT` | manoeuvre right→left |
| 4 | `LANE_CHANGE_RIGHT` | manoeuvre left→right |
| 5 | `OBSTACLE_STOP` | hold/creep near obstacle |
| 6 | `FINISHED` | end of track |
| 7 | `FAULT` | error / e-stop |

### 10.3 Lane & obstacle geometry (canonical, from description)

| Parameter | Value |
|---|---|
| Lane width | 0.40 m |
| Track length | 10.0 m |
| Number of lanes (Task 2) | 2 |
| Obstacle 1 | right lane, 4 m from start |
| Obstacle 2 | left lane, 8 m from start |
| Vehicle max width | 0.30 m |
| Start lane (Task 2) | right |

### 10.4 Frame names (TF)
`map → odom → base_link → {camera_link, imu_link, lidar_link, left_wheel, right_wheel}`

### 10.5 Command limits
`/cmd_vel` linear.x ∈ [0, v_max], angular.z ∈ [−ω_max, ω_max]. Values live in `config/robot_params.yaml`.

---

## 11. Performance Evaluation & Grading (from description §7)

| § | Criterion | Notes |
|---|---|---|
| 7.1 | Task success | completion of Task 1 and Task 2 |
| 7.2 | Navigation quality | lane-keeping accuracy, obstacle avoidance, control stability. **Wheel touching the tape = 1 point; 3 points = −1 mark** |
| 7.3 | Completion time & runs | **3 runs per task**, ≤5 min between runs, **best time** counts; ranked on combined best time |
| 7.4 | Bonus | 5 fastest teams: 1st=5, 2nd=4, 3rd=3, 4th=2, 5th=1 mark. MATLAB/Simulink part also earns bonus |

**Implication:** reliability (few tape touches) and speed both matter. Track "tape touches" and "best time"
in `docs/logs/` after every run.

---

## 12. Configuration SSOT

**Rule: nothing is hardcoded.** All physical constants, geometry, thresholds, and gains load from `config/`.
`config/README.md` documents the exact load order:

```
robot_params.yaml → sensor_params.yaml → lane_geometry.yaml → control_gains.yaml
```

| File | Owns |
|---|---|
| `config/robot_params.yaml` | wheelbase, wheel radius, mass, v_max, ω_max, encoder ticks |
| `config/sensor_params.yaml` | camera res/FOV, IMU rate, LiDAR/ultrasonic range, mounting |
| `config/lane_geometry.yaml` | lane width, track length, obstacle positions, tape thresholds |
| `config/control_gains.yaml` | PID gains, Pure Pursuit / Stanley parameters, lane-change tuning |

---

## 13. Ownership Matrix (fill member names)

> Fill in real names + student IDs before Week 1 closes. Every responsibility has a **lead** and a **support**.

| Responsibility | Lead | Support | Primary folder |
|---|---|---|---|
| Robot modeling and simulation | `<name>` | `<name>` | `modeling/`, `ros2_ws/src/amr_description` |
| ROS2 software architecture | `<name>` | `<name>` | `ros2_ws/src/*` |
| Perception and sensing | `<name>` | `<name>` | `ros2_ws/src/amr_perception` |
| State estimation | `<name>` | `<name>` | `ros2_ws/src/amr_localization` |
| Control system design | `<name>` | `<name>` | `ros2_ws/src/amr_control` |
| Hardware integration | `<name>` | `<name>` | `hardware/`, `firmware/`, `ros2_ws/src/amr_hardware` |
| Testing and validation | `<name>` | `<name>` | `data/`, `docs/logs/` |
| Documentation and reporting | `<name>` | `<name>` | `docs/report/` |

**Cross-cutting rule:** Documentation and reporting is the *only* responsibility allowed to restructure
`docs/report/`; everyone else submits material via pull request. ROS2 software architecture owns merges
to `main`.

---

## 14. Milestones

| ID | Target date | Milestone | Exit criteria (DoD) |
|---|---|---|---|
| **M0** | 17 Nov 2026 | Kickoff | repo + workspace created; responsibilities assigned; BOM issued |
| **M1** | 22 Nov 2026 (W1) | Foundation | robot model spawns in Gazebo; TF tree valid; interfaces built; hardware ordered |
| **M2** | 29 Nov 2026 (W2) | Sim Task 1 | closed-loop lane following on a straight lane in sim |
| **M3** | 06 Dec 2026 (W3) | Task 1 pass + HW bench | Task 1 passes in sim; chassis assembled; all sensors streaming on hardware |
| **M4** | 13 Dec 2026 (W4) | Sim Task 2 | obstacle detection + lane switching + return, in sim |
| **M5** | 20 Dec 2026 (W5) | HW both tasks | both tasks pass on the real vehicle |
| **M6** | **25 Dec 2026** | **Submission** | report + code + video + responsibility sheet + public repo |

---

## 15. Weekly Plan (guide steps per responsibility)

> 6 calendar weeks: **W1 16–22 Nov · W2 23–29 Nov · W3 30 Nov–6 Dec · W4 7–13 Dec · W5 14–20 Dec · W6 21–25 Dec 2026.**
> "Guide steps" are a starting checklist, not a ceiling — leads may extend them, but must not skip the DoD.

### Week 1 — Foundation & simulation skeleton  → **Milestone M1**

| Responsibility | Weekly task | Guide steps |
|---|---|---|
| Robot modeling and simulation | Choose & model the drivetrain; author the robot model | 1) Decide differential drive vs bicycle (recommend **differential drive**). 2) Derive kinematics; write `modeling/derivations/kinematics.md`. 3) Author `amr_description` URDF/xacro. 4) Put wheelbase/wheel radius/mass in `config/robot_params.yaml`. 5) Spawn in an empty Gazebo world; verify TF tree. |
| ROS2 software architecture | Stand up repo + ROS2 workspace + interfaces | 1) Create the `colcon` workspace and the 8 packages. 2) Freeze the node/topic list (§9.3). 3) Create `amr_interfaces` msgs (§10.1). 4) `colcon build` clean. 5) Commit the architecture doc + `README.md`. |
| Perception and sensing | Sensor selection + sim sensor config | 1) Spec camera (res/FOV), IMU rate, LiDAR/ultrasonic range. 2) Add camera + IMU + range sensor to the URDF. 3) Capture a sample lane image from sim. 4) Prototype HSV/edge thresholding on black tape in a scratch notebook. 5) Record findings in `docs/logs/`. |
| State estimation | Pick the estimation approach; odometry baseline | 1) Choose **odometry + EKF (IMU+encoders)**. 2) Read `/joint_states`; implement differential-drive odometry. 3) Configure `robot_localization` EKF. 4) Publish `/odom` + TF. 5) Compare against Gazebo ground truth. |
| Control system design | Control architecture decision | 1) Review PID vs Pure Pursuit vs Stanley for lane keeping. 2) Pick a lateral controller (recommend **Stanley** or **Pure Pursuit**) + a **speed PID**. 3) Define error signals (lateral offset, heading error). 4) Sketch the controller block diagram. 5) Seed gains in `config/control_gains.yaml`. |
| Hardware integration | BOM + procurement + mechanical concept | 1) Build the BOM (2 DC motors, drivers, encoders, IMU, camera, LiDAR/ultrasonic, compute unit, battery, chassis). 2) Verify **≤30 cm width** and rear-wheel drive. 3) Place orders **immediately** (lead time is the #1 risk). 4) CAD the chassis concept. 5) Draft the wiring/pinout plan. |
| Testing and validation | Test plan + logging | 1) Write the test matrix for Task 1 & Task 2. 2) Define KPIs: max lateral offset, tape touches, collisions, completion time. 3) Set up `rosbag` recording scripts. 4) Create sim test worlds (straight lane; two-lane). 5) Define pass/fail thresholds. |
| Documentation and reporting | Repo docs + report skeleton + responsibility sheet | 1) Create the 11-section report outline (§8, deliverable 9.1). 2) Write root `README.md` + folder READMEs. 3) Create `docs/logs/` meeting + milestone logs. 4) Draft the Team Responsibility Sheet (§9.4). 5) Create the **private** GitHub repo and push. |

### Week 2 — Perception, localization, first closed loop  → **Milestone M2**

| Responsibility | Weekly task | Guide steps |
|---|---|---|
| Robot modeling and simulation | Refine the model; validate kinematics | 1) Add mass/friction/wheel parameters. 2) Simulate a step input; compare pose vs Gazebo ground truth. 3) Fix model discrepancies. 4) Document model accuracy. |
| ROS2 software architecture | Node skeletons + launch/bringup | 1) Stub every node with correct pub/sub. 2) Write per-package launch files. 3) Write the top-level `amr_bringup` launch. 4) Verify with `rqt_graph` + `ros2 topic list`. 5) Add `param` files (no hardcoding). |
| Perception and sensing | Camera lane detection (Task 1) | 1) Implement ROI + perspective/colour pipeline for the black tape. 2) Fit lane center + tangent. 3) Publish `/perception/lane`. 4) Tune for the straight lane. 5) Visualise overlay for debugging. |
| State estimation | EKF fusion + state estimate | 1) Fuse IMU + wheel odometry in the EKF. 2) Tune process/measurement noise. 3) Publish `/state_estimate` + TF. 4) Compare estimate vs ground truth; log error. |
| Control system design | Implement lateral + speed control | 1) Implement the chosen lateral controller. 2) Implement speed PID. 3) Map outputs to `/cmd_vel`. 4) Initial gain tuning. 5) Log step responses. |
| Hardware integration | Assemble chassis + bench-test motors | 1) Receive/assemble the chassis. 2) Mount motors + encoders. 3) Bench-test the motor driver from the microcontroller. 4) Verify encoder counts/direction. 5) Report any BOM gaps to the hardware lead. |
| Testing and validation | First closed-loop Task 1 test | 1) Run lane following end-to-end in sim. 2) Record `rosbag`. 3) Measure lateral offset / tape touches / time. 4) File bugs to owners. 5) Regression-test after fixes. |
| Documentation and reporting | Write modeling + perception sections | 1) Draft §3 (math modeling) and §5 (perception). 2) Log this week's results + figures. 3) Update the responsibility sheet. 4) Post the weekly log. |

### Week 3 — Task 1 pass in sim + hardware bring-up  → **Milestone M3**

| Responsibility | Weekly task | Guide steps |
|---|---|---|
| Robot modeling and simulation | Finalize model; start optional MATLAB/Simulink | 1) Freeze the vehicle model. 2) Write the modeling section inputs for the reporting lead. 3) (Bonus) build a Simulink vehicle model. 4) (Bonus) mirror the controller in Simulink. 5) Track bonus progress. |
| ROS2 software architecture | Stabilize architecture; diagnostics | 1) Ensure all nodes launch from `amr_bringup`. 2) Add `/diagnostics` + node health. 3) Parameterize sim vs real. 4) Freeze the topic contract. 5) CI-style `colcon build` check. |
| Perception and sensing | Robust lane detection + obstacle detection skeleton | 1) Handle curves/lighting (adaptive thresholds, smoothing). 2) Add ROI/perspective robustness. 3) Stub obstacle detection from LiDAR/ultrasonic. 4) Publish `/perception/obstacles`. 5) Validate detection ranges. |
| State estimation | Tune EKF; IMU bias handling | 1) Calibrate/estimate IMU bias. 2) Tune noise covariances. 3) Validate heading estimate. 4) Handle wheel slip. 5) Log estimation error metrics. |
| Control system design | Tune gains; heading stability | 1) Tune lateral gains for lane-center tracking. 2) Tune speed PID. 3) Evaluate heading stability. 4) Document stability margins. 5) Freeze Task-1 gains in config. |
| Hardware integration | Complete platform; sensor streams on HW | 1) Finish chassis + compute-unit mounting. 2) Flash/verify firmware. 3) Bring camera/IMU/LiDAR/encoders up over ROS2. 4) Verify wireless (no cables) if using external processing. 5) Record a bench bring-up log. |
| Testing and validation | Task 1 acceptance in sim | 1) Run the Task-1 pass criteria repeatedly. 2) Confirm ≤ threshold lateral offset and 0 tape touches. 3) Record best time. 4) Freeze a regression bag. 5) Sign off M3. |
| Documentation and reporting | Write estimation + control sections | 1) Draft §6 (state estimation) and §7 (control design). 2) Insert result tables/figures. 3) Update responsibility sheet. 4) Weekly log. |

### Week 4 — Task 2 in sim + hardware sensor bring-up  → **Milestone M4**

| Responsibility | Weekly task | Guide steps |
|---|---|---|
| Robot modeling and simulation | (Bonus) MATLAB/Simulink task simulation | 1) Build a full-task Simulink sim (optional). 2) Compare with ROS2 results. 3) Document bonus work. 4) Otherwise support sim-to-real. 5) Keep model frozen. |
| ROS2 software architecture | Mission FSM + obstacle integration | 1) Implement the `mission_fsm_node` (§10.2). 2) Wire obstacle detection → lane change. 3) Wire return-to-right-lane. 4) Add timeouts/failsafe. 5) Verify topic communication end-to-end. |
| Perception and sensing | Complete obstacle detection + fusion | 1) Detect obstacles at the 4 m / 8 m fixed positions. 2) Fuse camera lane + range obstacle data. 3) Classify lane (left/right). 4) Publish confident `/perception/obstacles`. 5) Validate detection distance vs speed. |
| State estimation | Pose support for lane change | 1) Ensure a reliable pose/heading for the manoeuvre. 2) Add yaw-rate support if needed. 3) Validate during simulated lane change. 4) Log accuracy. |
| Control system design | Lane-change manoeuvre | 1) Implement right→left and left→right manoeuvres. 2) Re-center smoothly after the change. 3) Tune transition timing. 4) Avoid oscillation. 5) Freeze Task-2 gains. |
| Hardware integration | Bring up all HW sensors + drivers | 1) Bring camera/IMU/LiDAR/encoders up on the real vehicle. 2) Write/port ROS2 hardware drivers. 3) Verify `/cmd_vel` → motors. 4) Check sensor mounting/frames. 5) Fix wiring/mech issues. |
| Testing and validation | Task 2 acceptance in sim | 1) Run the full Task-2 sequence. 2) Confirm both switches + no collision. 3) Measure tape touches + time. 4) Record a regression bag. 5) Sign off M4. |
| Documentation and reporting | Write ROS2 + simulation methodology sections | 1) Draft §4 (simulation methodology) and §8 (ROS2 implementation). 2) Add architecture diagrams. 3) Weekly log. |

### Week 5 — Full hardware integration  → **Milestone M5**

| Responsibility | Weekly task | Guide steps |
|---|---|---|
| Robot modeling and simulation | Sim-to-real model validation | 1) Compare real logs with the sim model. 2) Adjust model parameters. 3) Document the gap. 4) Support HW tuning. 5) (Bonus) finalize Simulink. |
| ROS2 software architecture | Harden launch/config for hardware | 1) Split sim vs real launch/config. 2) Add startup/shutdown robustness. 3) Verify all topics on HW. 4) Add logging/record toggles. 5) Freeze the release branch. |
| Perception and sensing | Perception tuning on real camera | 1) Tune for real lighting/tape. 2) Validate obstacle detection on real obstacles. 3) Handle shadows/glare. 4) Freeze real-world thresholds in config. 5) Log detection reliability. |
| State estimation | EKF tuning on real IMU/encoders | 1) Tune noise on real data. 2) Validate heading/position. 3) Handle real wheel slip. 4) Log error metrics. |
| Control system design | Controller tuning on the real vehicle | 1) Tune lateral + speed on HW. 2) Tune lane change on HW. 3) Verify heading stability. 4) Freeze final gains. 5) Document. |
| Hardware integration | Full-system HW bring-up | 1) Assemble the complete vehicle. 2) Field-test Task 1 & Task 2. 3) Fix wiring/mechanical faults. 4) Prepare a pit kit (batteries, spares, tools). 5) Record run logs. |
| Testing and validation | Hardware validation of both tasks | 1) Run multiple trials per task. 2) Record tape touches + best times. 3) Regression-test fixes. 4) Compare against sim. 5) Report readiness. |
| Documentation and reporting | Write results + performance analysis; start video | 1) Draft §9 (experimental results) and §10 (performance analysis). 2) Write the video script (5–10 min, §9.3). 3) Weekly log. |

### Week 6 — Freeze, validate, document, submit  → **Milestone M6 (25 Dec 2026)**

| Responsibility | Weekly task | Guide steps |
|---|---|---|
| Robot modeling and simulation | Finalize model + MATLAB bonus | 1) Freeze model docs. 2) (Bonus) finalize Simulink + results. 3) Confirm bonus deliverables. 4) Support final report figures. |
| ROS2 software architecture | Code freeze + reproducibility | 1) Freeze code; clean packages. 2) Final `colcon build` on a clean machine. 3) Verify `README` run instructions. 4) Ensure worlds + launch files included. 5) Tag the release. |
| Perception and sensing | Final perception freeze | 1) Confirm thresholds in `config/`. 2) Re-run Task 1 & Task 2 perception checks. 3) Remove debug code. 4) Document final pipeline. |
| State estimation | Final estimation validation | 1) Re-validate the EKF on the final data. 2) Freeze parameters. 3) Document metrics. |
| Control system design | Final control validation | 1) Confirm final gains. 2) Record best runs. 3) Document stability/performance. |
| Hardware integration | Final hardware check | 1) Verify battery/charging. 2) Pack spares + tools. 3) Confirm wireless operation. 4) Run a full dry-run. 5) Checklist sign-off. |
| Testing and validation | Final acceptance test | 1) 3 runs per task, best time recorded. 2) Capture data + video footage. 3) Verify no tape-touch penalty risk. 4) Produce the final results table. 5) Sign off. |
| Documentation and reporting | Finalize & submit | 1) Finalize the report (all 11 sections). 2) Finalize the responsibility sheet (§9.4). 3) Produce/edit the 5–10 min video. 4) **Make the GitHub repo public at submission.** 5) Submit everything by **25 Dec 2026**. |

---

## 16. Risk Register

| Risk | Impact | Mitigation | Owner (responsibility) |
|---|---|---|---|
| Hardware parts arrive late | blocks M3/M5 | order in W1; identify local suppliers; keep a sim-first plan | Hardware integration |
| Camera lane detection fails under real lighting | fails Task 1/2 | adaptive HSV/edge + test on-site in W5; keep ROI robust | Perception and sensing |
| Sim-to-real gap | HW under-performs | validate model early (W3/W5); tune on HW | Robot modeling and simulation / Control system design |
| Lane change oscillates / touches tape | grading penalty | tune on HW in W5; limit yaw rate | Control system design |
| Wheel touches tape (3 pts = −1 mark) | grade loss | prioritize reliability over speed in W5 | Testing and validation |
| Team member unavailability | slips milestones | lead + support on every responsibility (§13) | all |
| Scope creep (bonus MATLAB) | delays core | treat bonus as optional; only after M4 | Robot modeling and simulation |

---

## 17. Git & Repository Conventions

- **Remote:** `https://github.com/amaryasser3210-sketch/dr-drive.git`
- **Branching:** `main` (protected) ← `dev` ← feature branches `feat/<area>-<short>`; hotfixes `fix/<area>`.
- **Commits:** Conventional Commits — `feat(perception): add HSV lane threshold`, `fix(control): clamp yaw rate`.
- **Merges:** ROS2 software architecture owns merges to `main`. No direct pushes to `main`.
- **Line endings:** LF enforced for source (`.gitattributes`).
- **Binaries:** `.pdf .png .jpg .mp4 .bag .mat .slx .stl .step .onnx` tracked via **Git LFS**.
- **Ignored:** `build/ install/ log/ __pycache__/ *.pyc .vscode/` (see `.gitignore`).
- **Visibility:** repo **private until the submission deadline**, then **public at submission** (§9.2).

---

## 18. Definition of Done (submission checklist)

- [ ] Task 1 and Task 2 both pass in **simulation** (ROS2 + Gazebo).
- [ ] Task 1 and Task 2 both pass on **hardware**.
- [ ] `config/` is the only place parameters live (no hardcoding).
- [ ] All 8 ROS2 packages build cleanly and are documented.
- [ ] Technical report covers all **11** required sections (§9.1).
- [ ] Project video (5–10 min) shows robot, sim, ROS2 architecture, hardware, both tasks.
- [ ] Team Responsibility Sheet completed (§9.4).
- [ ] Root `README` explains how to run the project.
- [ ] GitHub repo **public** at submission, containing code + worlds + launch files.
- [ ] (Optional) MATLAB/Simulink bonus delivered.
- [ ] Submitted by **25 / 12 / 2026**.

---

*Handbook version 1.1 — generated for the MCT443s course project. Keep this file authoritative; log changes in `docs/logs/`.*
