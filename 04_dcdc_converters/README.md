# 04 · Automotive Switched-Mode Power Supplies (SMPS)

[![Compliance: ISO 16750-2](https://img.shields.io/badge/Compliance-ISO%2016750--2-red.svg)](#)
[![Compliance: CISPR 25](https://img.shields.io/badge/EMC-CISPR%2025%20Class%205-blue.svg)](#)

Automotive-grade non-isolated DC-DC converters engineered for cold-crank ride-through, load dump suppression, and stable closed-loop feedback.

---

## ⚡ Core Engineering Focus

1. **Synchronous Buck Converter Optimization:**
   - Minimizing high-frequency switching hot-loop perimeter ($< 1\,\text{cm}^2$) across input decoupling capacitors and half-bridge MOSFETs.
2. **Cold-Crank & Load-Dump Compliance (ISO 16750-2):**
   - Coupled-inductor SEPIC and wide-$V_{\text{in}}$ boost designs maintaining regulated $12\,\text{V}$ rails through severe $3.2\,\text{V}$ engine start dips and $36\,\text{V} - 42\,\text{V}$ clamped load-dump transients.
3. **Small-Signal Feedback & Stability:**
   - Type-II and Type-III transconductance error amplifier compensation.
   - Right-Half-Plane (RHP) zero tracking and phase margin preservation ($> 45^\circ$, gain margin $> 10\,\text{dB}$) in continuous conduction mode (CCM).

---

## 📂 Subdirectory Contents

- `/buck_sync_24v_5v`: Synchronous buck converter simulation decks, inductor volt-microsecond design sheets, and BOM selections.
- `/boost_12v_24v`: Automotive boost stage models with RHP zero stabilization networks.
- `/sepic_automotive`: Continuous SEPIC converter files providing seamless buck-boost operation during transient battery fluctuations.

---

## 📑 Associated Publications & Lead Magnets

- **Lead Magnet:** `Doc ID: EMH-PE-CAL-004` (Automotive Synchronous Buck WCCA & Loop Compensation Matrix)
- **Technical Masterclass:** [Automotive DC-DC Converters: Cold-Crank Ride-Through, Load Dump, and Feedback Stability](https://electromaestrohub.blogspot.com/)