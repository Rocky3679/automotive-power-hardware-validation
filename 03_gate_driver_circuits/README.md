# 03 · Gate Driver Architectures & Shoot-Through Protection

[![Topology: Half--Bridge](https://img.shields.io/badge/Topology-Isolated%20Half--Bridge-blue.svg)](#)
[![Standards: ISO 16750-2](https://img.shields.io/badge/Standard-ISO%2016750--2-orange.svg)](#)

High-voltage isolated gate drivers, parasitic $dV/dt$ false turn-on suppression, and bootstrap charging dynamics for SiC and silicon MOSFETs.

---

## ⚡ Core Engineering Focus

1. **Parasitic $dV/dt$ Induced Turn-On (Miller Effect):**
   - Analysis of capacitive displacement current ($i_{\text{disp}} = C_{gd} \cdot \frac{dV}{dt}$) charging the gate terminal during bridge leg transitions.
2. **Active Miller Clamp (AMC) Implementation:**
   - Low-impedance internal or external bipolar/MOSFET clamp pulling the gate to ground/negative rail whenever $V_{gs} \le 2.0\,\text{V}$.
3. **Negative Gate Voltage Biasing:**
   - Implementation of $-3\,\text{V}$ to $-5\,\text{V}$ negative turn-off bias for high-speed wide-bandgap (WBG) power switches.
4. **Bootstrap Supply Sizing & Duty Cycle Limits:**
   - Analytical sizing of $C_{\text{boot}}$ to ensure minimum forward voltage margin during sustained high-side conduction.

---

## 📂 Subdirectory Contents

- `/kicad`: Reference schematics for galvanically isolated gate drivers with integrated desaturation (DESAT) fault detection.
- `/docs`: Worst-Case Circuit Analysis (WCCA) calculation sheets for gate resistor ($R_{g,\text{on}} / R_{g,\text{off}}$) selection and thermal dissipation.

---

## 📑 Associated Publications & Lead Magnets

- **Lead Magnet:** `Doc ID: EMH-PE-CAL-002` (Half-Bridge Gate Driver Timing & Bootstrap Sizing Matrix)
- **Technical Masterclass:** [Gate Driver Design: Active Miller Clamping, Bootstrap Calculations, and Shoot-Through Elimination](https://electromaestrohub.blogspot.com/)