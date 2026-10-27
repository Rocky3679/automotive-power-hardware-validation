# 01 · System Grounding, Return Paths & EMC Mitigation

[![Standards: CISPR 25](https://img.shields.io/badge/EMC-CISPR%2025%20Class%205-blue.svg)](#)
[![Standards: ISO 16750-2](https://img.shields.io/badge/Transient-ISO%2016750--2-orange.svg)](#)
[![Standards: IEC 61000-4-2](https://img.shields.io/badge/ESD-IEC%2061000--4--2-green.svg)](#)

Engineering reference architecture, 4-layer stackup rules, and return path physics for automotive mixed-signal power converters.

---

## ⚡ Core Engineering Focus

1. **High-Frequency Return Path Dynamics:** 
   - Modeling return current transitions at $f_c \approx 100\,\text{kHz}$ from least resistance to least inductance.
   - Slot antenna radiation mitigation ($L_{\text{loop}} \approx 5.08 \cdot h \cdot \ln(w/h)\,\text{nH/inch}$) to meet CISPR 25 Class 5 limits.
2. **Unified Ground Partitioning:**
   - Single continuous 0V reference plane strategy with strict geographic zone isolation (Power Stage | Digital MCU | Analog Front-End).
3. **Automotive Chassis Decoupling:**
   - High-voltage isolation network: $1\,\text{M}\Omega$ static bleed resistor in parallel with $10\,\text{nF} / 2\,\text{kV}$ ceramic RF shunt capacitor.
4. **Transient & ESD Protection (IEC 61000-4-2):**
   - Connector-edge low-inductance TVS diodes tied directly to chassis ground using thermal via stitching.

---

## 📂 Subdirectory Contents

- `/kicad`: 4-Layer reference board layout files (`.kicad_sch`, `.kicad_pcb`), stackup definitions, and Design Rule Check (DRC) configurations. *(Work In Progress)*
- `/docs`: Mechanical mounting hole earthing details, return-via stitching guidelines, and impedance calculators.

---

## 📑 Associated Publications & Lead Magnets

- **Lead Magnet:** `Doc ID: EMH-HW-CKL-001 · Rev 1.0` (1-Page PCB Grounding & EMC Mitigation Checklist)
- **Technical Deep-Dive:** [Demystifying System Grounding: From Heavy Pipe & Plate Earthing to High-Speed PCB Noise Mitigation](https://electromaestrohub.blogspot.com/2026/10/electrical-earthing-grounding-pipe-plate-pcb.html)