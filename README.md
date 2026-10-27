# Automotive Power Hardware Design & Validation Suite

[![Standards: CISPR 25](https://img.shields.io/badge/EMC-CISPR%2025%20Class%205-blue.svg)](#-standards-compliance-matrix)
[![Standards: ISO 16750-2](https://img.shields.io/badge/Transient-ISO%2016750--2-orange.svg)](#-standards-compliance-matrix)
[![Standards: IEC 61000-4-2](https://img.shields.io/badge/ESD-IEC%2061000--4--2-green.svg)](#-standards-compliance-matrix)
[![EDA: KiCad 8.0+](https://img.shields.io/badge/EDA-KiCad%208.0%2B-blueviolet.svg)](https://www.kicad.org/)
[![Sim: LTspice](https://img.shields.io/badge/Simulation-LTspice-red.svg)](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)
[![Documentation: Electro Maestro Hub](https://img.shields.io/badge/Docs-Electro%20Maestro%20Hub-yellow.svg)](https://electromaestrohub.blogspot.com)

Production-grade hardware reference designs, LTspice verification testbenches, and automated analytical calculation scripts for automotive low-voltage ($12\,\text{V}$ / $24\,\text{V}$ / $48\,\text{V}$) and electric powertrain subsystems. 

This repository serves as an open-source engineering reference for **Automotive Hardware Design, Test, and Validation Engineers**, bridging first-principles circuit physics, Worst-Case Circuit Analysis (WCCA), and physical test execution aligned with Design Verification Plan and Report (DVP&R) guidelines.

---

## 📋 Standards Compliance Matrix

All circuit topologies, PCB layouts, and simulation testbenches in this repository are designed to adhere to the following automotive and industrial validation standards:

| Standard | Scope / Description | Implemented Countermeasure |
| :--- | :--- | :--- |
| **CISPR 25 Class 5** | Radio disturbance characteristics for automotive receivers ($150\,\text{kHz} - 2.5\,\text{GHz}$). | Symmetrical hot-loop layout, 4-layer low-inductance ground planes, common-mode & differential-mode filtering. |
| **ISO 16750-2** | Environmental conditions and electrical testing for $12\,\text{V} / 24\,\text{V}$ electrical equipment. | Cold-crank ride-through ($3.2\,\text{V}$), load dump protection ($U_s^* = 36\,\text{V} - 42\,\text{V}$), reverse polarity clamping. |
| **ISO 7637-2** | Electrical transient conduction along automotive supply lines. | TVS suppression arrays, negative transient clamping (Pulse 1, 2a, 3a/b). |
| **IEC 61000-4-2** | Electrostatic Discharge (ESD) immunity ($\pm 8\,\text{kV}$ contact, $\pm 15\,\text{kV}$ air). | Connector-edge low-inductance TVS diodes with dedicated chassis ground return stitching. |
| **IPC-2152** | Standard for determining current carrying capacity in printed board designs. | Analytical trace sizing and thermal via arrays configured for $< 30^\circ\text{C}$ thermal rise at full continuous load. |

---

## 📂 Repository Architecture

```text
automotive-power-hardware-validation/
│
├── 01_system_grounding_emc/            # 4-Layer Grounding, Return Paths & Shielding
│   ├── kicad/                         # KiCad 8.0 reference PCB layout & schematics
│   └── README.md                      # Return path physics, loop inductance & chassis RC tie
│
├── 02_power_semiconductors_snubbers/   # Switching Dynamics & Parasitic Ringing Suppression
│   ├── ltspice/                       # Diode trr, MOSFET dV/dt & snubber transient decks
│   └── python/                        # Automated RC/RCD snubber parameter solvers
│
├── 03_gate_driver_circuits/            # Isolated Gate Drivers & Shoot-Through Protection
│   ├── kicad/                         # Half-bridge driver reference board (SiC/Si MOSFET)
│   └── docs/                          # Active Miller clamp, bootstrap sizing & negative rails
│
├── 04_dcdc_converters/                # Automotive Switched-Mode Power Supplies (SMPS)
│   ├── buck_sync_24v_5v/              # Synchronous buck hot-loop optimization (CISPR 25)
│   ├── boost_12v_24v/                 # Type-III loop compensation & RHP zero mitigation
│   └── sepic_automotive/              # Cold-crank/Load-dump ride-through SEPIC converter
│
├── 05_inverters_motor_control/        # 3-Phase Traction Drives & Vector Modulation
│   ├── svpwm_c_engine/                # ANSI C fixed-point (Q15) 7-segment SVPWM firmware
│   └── foc_simulink/                  # Closed-loop PMSM/BLDC Field-Oriented Control model
│
└── README.md                          # Master repository documentation
```

---

## 🔬 Subsystem Technical Breakdown

### 01 · System Grounding, Return Paths & EMC (`01_system_grounding_emc`)
* **Core Physics:** Transition frequency analysis ($f_c \approx 100\,\text{kHz}$) where return currents migrate from the path of least resistance to the path of least inductance directly under signal conductors.
* **Key Deliverables:**
  * 4-layer stackup design (`SIG-GND-PWR-SIG`) with an uninterrupted Layer 2 ground reference.
  * Slot antenna radiation prevention (eliminating $20\,\text{dB} - 30\,\text{dB}$ emissions spikes across split planes).
  * High-voltage chassis decoupling: Parallel $1\,\text{M}\Omega$ static bleed resistor and $10\,\text{nF} / 2\,\text{kV}$ ceramic RF shunt capacitor network.

### 02 · Power Semiconductors & Snubbers (`02_power_semiconductors_snubbers`)
* **Core Physics:** Parasitic extraction of bridge switch-node inductances ($L_\sigma$) and switch output capacitances ($C_{\text{oss}}$). Reverse recovery charge ($Q_{rr}$) transient suppression.
* **Key Deliverables:**
  * Automated Python damping solver calculating optimal resistor-capacitor snubber values ($R_{\text{snub}} = \sqrt{L/C}$, $C_{\text{snub}} = 2 \cdot C_{\text{oss}}$) based on observed oscilloscope ring frequency.
  * LTspice circuit models comparing un-snubbered vs. critically damped hard-switched nodes.

### 03 · Gate Driver Architectures (`03_gate_driver_circuits`)
* **Core Physics:** Parasitic $dV/dt$ capacitive coupling across switch Miller capacitance ($C_{\text{gd}}$) causing false gate turn-on and catastrophic DC-bus shoot-through.
* **Key Deliverables:**
  * Active Miller Clamp (AMC) circuit implementations sinking transient currents directly to ground when gate voltage drops below $2.0\,\text{V}$.
  * Negative turn-off gate bias generation ($-3\,\text{V}$ to $-5\,\text{V}$) for SiC/GaN fast-switching topologies.
  * Dynamic bootstrap capacitor ($C_{\text{boot}}$) sizing and refresh timing analysis for high-side gate power delivery.

### 04 · Automotive DC-DC Converters (`04_dcdc_converters`)
* **Topologies Covered:** Synchronous Buck, Continuous-Conduction Boost, and Coupled-Inductor SEPIC.
* **Validation Focus:**
  * **Hot-Loop Sizing:** Minimizing high-frequency $di/dt$ loop area ($< 1\,\text{cm}^2$) across input bypass capacitors, high-side MOSFETs, and low-side sync rectifiers.
  * **ISO 16750-2 Compliance:** SEPIC topology designed to maintain regulated $12\,\text{V}$ output through severe $3.2\,\text{V}$ cold-crank dips and $40\,\text{V}$ load-dump spikes.
  * **Loop Stability:** Right-Half-Plane (RHP) zero phase-margin preservation using Type-II and Type-III transconductance amplifier networks.

### 05 · Motor Inverters & Modulation Control (`05_inverters_motor_control`)
* **Core Physics:** Orthogonal coordinate transformations ($\text{Clarke: } abc \to \alpha\beta$, $\text{Park: } \alpha\beta \to dq$) for decoupled flux ($i_d$) and torque ($i_q$) regulation.
* **Key Deliverables:**
  * Symmetrical 7-segment Space Vector PWM (SVPWM) C engine achieving $+15.47\%$ higher fundamental DC-bus utilization over scalar SPWM.
  * Hardware dead-time insertion ($1\,\mu\text{s} - 2\,\mu\text{s}$) with analytical volt-second error compensation to eliminate 6th harmonic torque ripple.
  * Closed-loop current-loop bandwidth tuning ($f_{\text{bw}} \approx 1\,\text{kHz} - 2.5\,\text{kHz}$) with cross-coupling feedforward decoupling.

---

## 🛠️ Toolchain & Validation Environment

| Domain | Tool / Software | Version | Purpose |
| :--- | :--- | :--- | :--- |
| **EDA / CAD** | KiCad EDA | 8.0+ | Schematic capture, controlled-impedance layout, DRC/ERC verification. |
| **SPICE Simulation** | LTspice (Analog Devices) | 24.x | Time-domain transient verification, step-response, switching losses. |
| **Modulation / Control** | MATLAB & Simulink | R2024b | Fixed-point FOC model-based simulation, state-space stability analysis. |
| **Firmware Execution** | ANSI C / IQ-Math | C99 / Q15 | Microcontroller-agnostic motor control and PWM generation algorithms. |
| **Data Processing** | Python (NumPy, SciPy, Matplotlib) | 3.10+ | Snubber calculation, bode plotting, thermal resistance calculations. |

---

## 📑 Master Document Release Register (EDRR)

Every hardware module and layout guide in this repository is tracked against a formal Engineering Document Register:

* `EMH-HW-CKL-001` · [1-Page PCB Grounding, Return Paths & EMC Mitigation Checklist](01_system_grounding_emc/)
* `EMH-PE-CAL-002` · Half-Bridge Gate Driver Timing & Bootstrap Sizing Matrix
* `EMH-HW-CAL-003` · Thermal Via Sizing & Heat Dissipation Analytical Calculator
* `EMH-PE-CAL-004` · Automotive Synchronous Buck WCCA & Loop Compensation Matrix
* `EMH-MD-CKL-005` · Space Vector PWM (SVPWM) Sector Mapping & Dwell Time Reference

---

## 🔗 Technical Publications & Deep-Dives

Theoretical derivations, mathematical proofs, and comprehensive bench validation waveforms corresponding to each subfolder are published as peer-level technical masterclasses on:

👉 **[Electro Maestro Hub](https://electromaestrohub.blogspot.com)**

---

## 📜 License & Usage

This repository is published under the [MIT License](LICENSE). Hardware layouts, schematics, and simulation decks are distributed for educational and engineering development use.