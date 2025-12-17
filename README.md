# Electrical_speed_controller
ESC module made for school collab project

# ESC Project – Current Status Overview

This repository contains the **hardware design and manufacturing outputs** for the ESC (Electronic Speed Controller) project.  
The focus so far has been on **power stage architecture, safety mechanisms, and manufacturable PCB design**.

---

## Project Scope (So Far)

- Target application: **BLDC motor control ESC**
- Focus: **hardware bring-up, safety, and power integrity**
- Firmware is **out of scope for this stage** (handled separately)

---

## Key Features Implemented

### Power & Safety Architecture

- **Mechanical E-Stop integration**
  - Hardware-level cut-off via relay
  - Independent of firmware execution

- **Relay-based power isolation**
  - Normally-Closed (NC) → Normally-Open (NO) switching
  - Triggered via controller-side IRQ signal

- **Fail-safe philosophy**
  - Loss of control signal defaults to power cut

See:
- `schematics/ESC_Controller_Schematic.pdf`

---

### Power Stage & Layout

- Dedicated **power stage region** separated from control logic
- Short, low-inductance **high-current loops**
- Local high-frequency decoupling close to switching devices
- Ground strategy designed for mixed-signal environment

See:
- `schematics/ESC_Controller_Schematic.pdf`
- `gerber/`

---

### Control & Interfaces

- MCU-based control architecture
- Explicit signal routing for:
  - PWM / gate control
  - IRQ / safety lines
- Clear pin labeling to support CubeIDE configuration

See:
- `schematics/ESC_Controller_Schematic.pdf`

---

### Manufacturing Readiness

- Full **BOM prepared** for sourcing and cost tracking
- **Gerber package generated** for fabrication
- Assembly intent clearly reflected in PCB layout

See:
- `BOM/`
- `gerber/`
- `PCB_Assembly/`

---

## Repository Structure Guide

├── PCB_Assembly/ # Assembly drawings, board views, reference images

├── BOM/ # Bill of Materials (manufacturer + part numbers)
├── schematics/ # PDF schematics for review and debugging

├── gerber/ # Fabrication-ready Gerber files

└── README.md


Use this as the **entry point** when reviewing or onboarding.

---

## TODO / Next Steps

### Hardware

- Peer review of schematics (power + safety paths)
- ERC / DRC final pass before fabrication
- Verify relay ratings vs load conditions
- Double-check ground return paths for current sensing

### Manufacturing

- Finalize BOM substitutions (availability check)
- Panelization (if required by fab)
- Assembly notes for sensitive components (MOSFETs, shunts)

### Bring-Up Preparation

- Define test points and probing plan
- Power-up checklist (pre- and post-relay)
- Fault-injection tests (E-stop, lost IRQ, brownout)

---

## Notes for Reviewers

- This is a **hardware-focused milestone**
- Functional firmware behavior is **not required** to evaluate safety or layout correctness
- Pay particular attention to:
  - Power cut-off logic
  - Grounding and current paths
  - Clear separation of noisy vs sensitive signals
