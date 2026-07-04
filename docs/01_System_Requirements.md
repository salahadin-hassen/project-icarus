# Project Icarus — System Requirements Specification (V1)

## 1. System Purpose
Project Icarus is a modular flight dynamics and control simulation system used to model aircraft motion, test control algorithms, and evaluate system responses in a controlled virtual environment.

---

## 2. System Overview

The system consists of four core subsystems:

### 2.1 Simulation Engine
Responsible for physics-based state propagation.

- Computes motion using Newtonian mechanics
- Updates state at fixed timestep (dt)
- Maintains aircraft state vector:
  - position (x, y, z)
  - velocity (vx, vy, vz)
  - orientation (roll, pitch, yaw)
  - angular velocity

---

### 2.2 Control System
Generates control inputs based on system error.

- Supports PID controller (V1)
- Inputs:
  - desired state (setpoint)
  - current state
- Outputs:
  - control forces / moments

---

### 2.3 Experiment Framework
Runs reproducible simulations.

- Loads configuration files (YAML)
- Executes simulation runs
- Stores results (JSON or CSV)
- Ensures repeatability of experiments

---

### 2.4 Telemetry System (Future V1.1)
Captures and logs system state over time.

- Time-series logging
- Metrics extraction (error, overshoot, settling time)
- Optional visualization layer

---

## 3. Functional Requirements

### FR1 — Simulation Update Loop
System must update state using a fixed timestep simulation loop.

### FR2 — Control Feedback Loop
System must compute control output based on current error at each timestep.

### FR3 — Experiment Execution
System must support running simulations via a single experiment entry point.

### FR4 — Configuration Driven Runs
All experiment parameters must be configurable via YAML files.

### FR5 — Result Storage
All experiment outputs must be saved in structured format for later analysis.

---

## 4. Non-Functional Requirements

### NFR1 — Determinism
Same configuration must produce identical results.

### NFR2 — Modularity
Each subsystem must be independently replaceable.

### NFR3 — Extensibility
System must allow future addition of:
- advanced controllers (LQR, MPC)
- 6-DOF aircraft models
- real-time visualization

---

## 5. Constraints

- No external physics engine dependency in V1
- Python-based implementation only
- CPU-only execution for baseline version

---

## 6. Success Criteria (V1)

System is considered functional if:

- A simulated object moves under applied forces
- PID controller stabilizes at least one variable (altitude or angle)
- Experiment runner executes without manual intervention
- Results are reproducible from config alone