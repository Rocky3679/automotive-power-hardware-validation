# 05 · Motor Inverters & Modulation Control

[![Control: FOC](https://img.shields.io/badge/Control-Field--Oriented%20Control-purple.svg)](#)
[![Modulation: SVPWM](https://img.shields.io/badge/Modulation-7--Segment%20SVPWM-brightgreen.svg)](#)
[![Firmware: ANSI C](https://img.shields.io/badge/Firmware-ANSI%20C%20(Q15)-blue.svg)](#)

3-Phase traction inverter algorithms, vector coordinate transformations, and ANSI C fixed-point Space Vector PWM (SVPWM) firmware.

---

## ⚡ Core Engineering Focus

1. **Orthogonal Coordinate Transformations:**
   - Simplified forward and inverse Clarke ($\alpha\beta$) and Park ($dq0$) transformations for decoupled rotor flux ($\lambda_d$) and electromagnetic torque ($T_e$) control.
2. **Symmetrical 7-Segment SVPWM:**
   - Voltage space vector synthesis achieving $+15.47\%$ higher fundamental DC-bus voltage utilization compared to traditional Sinusoidal PWM (SPWM).
3. **Inverter Dead-Time & Non-Linearity Compensation:**
   - Analytical volt-second dead-time error correction algorithms eliminating 5th and 7th harmonic phase currents and 6th harmonic torque ripple.
4. **Current-Loop Tuning:**
   - Internal Model Control (IMC) bandwidth tuning for cross-coupling feedforward decoupling in permanent magnet synchronous motors (PMSM).

---

## 📂 Subdirectory Contents

- `/svpwm_c_engine`: Production-grade ANSI C (C99) implementation using Q15 fixed-point arithmetic for fast execution on embedded MCUs.
- `/foc_simulink`: MATLAB / Simulink closed-loop PMSM vector control model featuring speed and current feedback loops.

---

## 📑 Associated Publications & Lead Magnets

- **Lead Magnet:** `Doc ID: EMH-MD-CKL-005` (Space Vector PWM Sector Mapping & Dwell Time Reference)
- **Technical Masterclasses:** 
  - [Space Vector PWM (SVPWM) Explained: Sector Mapping, Dwell Times, and Inverter Harmonics](https://electromaestrohub.blogspot.com/)
  - [Field-Oriented Control (FOC) Demystified: Clarke, Park, and Current Loop Tuning](https://electromaestrohub.blogspot.com/)