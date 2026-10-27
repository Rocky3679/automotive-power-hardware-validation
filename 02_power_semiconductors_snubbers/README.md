# 02 · Power Semiconductors & Snubber Topologies

[![EDA: LTspice](https://img.shields.io/badge/Simulation-LTspice-red.svg)](#)
[![Language: Python 3.10+](https://img.shields.io/badge/Language-Python%203.10%2B-yellow.svg)](#)

Switching dynamics, reverse recovery charge ($Q_{rr}$) damping, and analytical snubber network design for hard-switched power converters.

---

## ⚡ Core Engineering Focus

1. **Parasitic Loop Extraction:**
   - Extraction and damping of parasitic switch-node ringing caused by stray loop inductance ($L_\sigma$) and switch output capacitance ($C_{\text{oss}}$).
2. **Snubber Parameter Solvers:**
   - Analytical calculation of RC and RCD snubbers to suppress transient overshoots below device breakdown ratings ($V_{\text{DS,max}}$) while minimizing switching power loss:
     $$R_{\text{snub}} = \sqrt{\frac{L_\sigma}{C_{\text{oss}}}}, \quad C_{\text{snub}} \ge 2 \cdot C_{\text{oss}}$$
3. **Flyback & Diode Reverse Recovery:**
   - Time-domain simulation of diode reverse recovery time ($t_{rr}$) and peak reverse recovery current ($I_{rrm}$) during rapid turn-off transients ($di/dt > 500\,\text{A}/\mu\text{s}$).

---

## 📂 Subdirectory Contents

- `/ltspice`: Hard-switched bridge leg models, snubber loss comparison decks, and time-domain transient testbenches.
- `/python`: Automated Python solvers for calculating optimal RC damper values from observed oscilloscope resonant ring frequencies.

---

## 📑 Associated Publications

- **Technical Masterclass:** [Power Diodes & Flyback Rectification: Reverse Recovery Time, Snubbers, and Freewheeling Action](https://electromaestrohub.blogspot.com/)