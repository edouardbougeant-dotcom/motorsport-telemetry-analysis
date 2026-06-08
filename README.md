#  Motorsport Telemetry Analysis
 
![Python](https://img.shields.io/badge/Python-3.x-blue)
![FastF1](https://img.shields.io/badge/FastF1-telemetry-red)
![Status](https://img.shields.io/badge/status-portfolio-success)
![License](https://img.shields.io/badge/License-MIT-green)
 
> Formula 1 telemetry analysis and vehicle-dynamics simulation built with **FastF1** — driver braking comparison, a SciPy-calibrated point-mass lap-time model, and aerodynamic coefficient estimation, all brought together in an interactive dashboard.
 
## Overview
 
What separates a fast lap from a slow one? This project answers that question using real Formula 1 telemetry from the 2023 season, accessed through the **FastF1** API. It moves from pure data analysis — comparing how two drivers attack the same corner — to physics-based simulation, rebuilding a full lap from the equations of motion, and finally to aerodynamic estimation. Together these form the core toolkit of a **data & performance engineer**. Every analysis is cross-checked against the methods described in Jorge Segers' *Analysis Techniques for Racecar Data Acquisition*.
 
## Key Results
 
-  **Physics-based lap-time model validated within ~2%.** A point-mass model with a friction-circle traction-limited corner exit, calibrated on *independent* observables — downforce on measured corner speeds, drag on the measured top speed (350 km/h) rather than on the lap time itself — **predicts** Carlos Sainz's real Monza pole lap (**1:20.294**) to within **~2% (1.6 s)**. Calibrated coefficients: Cx = 0.748, Cl = 3.023.
- **Braking analysis — Sainz vs Stroll (Monza Q).** Sainz brakes **later at every single braking zone**, up to **+30 m at Lesmo 1** (≈ 
+0.43s on one corner). A combined-G "valley" pinpoints exactly where Stroll brakes too early and leaves grip unused.
- **Aerodynamic analysis (Monza & Monaco).** DRS cuts drag by **18.6%** at Monza (Cx 1.06 → 0.87), worth roughly **+23 km/h** of top speed — in line with Segers' 15–25% range. Comparing the estimated drag coefficients across circuits also captures each car's setup philosophy: Monaco's high-downforce configuration runs an estimated Cx **~76% higher** than Monza's low-drag setup (≈ 1.52 vs 0.87).
- **Interactive dashboard.** All key analyses combined into a single explorable Plotly / HTML view.
## Project Structure
 
```
motorsport-telemetry-analysis/
├── notebooks/
│   ├── 01_exploration_fastf1.ipynb
│   ├── 02_lap_comparison_monaco_2023.ipynb
│   ├── 03_gg_diagram.ipynb
│   ├── 04_multi_channel_overlay_monaco_2023.ipynb
│   ├── 05_multi_channel_overlay_monza_2023.ipynb
│   ├── 06_tyre_analysis_bahrain_2023.ipynb
│   ├── 07_braking_analysis_monza_2023.ipynb
│   ├── 08_point_mass_model.ipynb
│   ├── 09_aero_analysis.ipynb
│   ├── 10_track_map_analysis.ipynb
│   └── 11_interactive_dashboard.ipynb
├── outputs/
│   └── motorsport_dashboard.html
├── requirements.txt
└── README.md
```
 
## Technical Stack
 
- **Python** — core language
- **FastF1** — Formula 1 telemetry data acquisition
- **NumPy / pandas** — numerical processing and data wrangling
- **Matplotlib / Plotly** — static and interactive visualisation
- **SymPy** — symbolic derivation of the vehicle-dynamics equations
- **SciPy** — model calibration (`scipy.optimize`)
## Installation
 
```bash
git clone https://github.com/edouardbougeant-dotcom/motorsport-telemetry-analysis.git
cd motorsport-telemetry-analysis
pip install -r requirements.txt
jupyter notebook
```
 
## Methodology
 
The project is organised in five phases:
 
- **Foundations** — Python / FastF1 setup and first telemetry analyses (speed, throttle, brake) on Monaco 2023.
- **Driver & Performance Analysis** — GG diagrams (friction circle), multi-channel lap overlays, and a detailed braking comparison (Sainz vs Stroll, Monza).
- **Simulation & Vehicle Dynamics** — a quasi-static point-mass lap-time model derived with SymPy, calibrated against real telemetry with SciPy, plus aerodynamic coefficient estimation from top-speed data.
- **Track Mapping** — telemetry channels (braking, speed) superimposed on the circuit layout to give a clear spatial reference of where events happen on track, following Segers (Ch. 2.2.2).
- **Portfolio & Publication** — interactive dashboard and documentation.
## Limitations
 
Working from publicly available telemetry imposes some honest constraints:
 
- **GPS-derived accelerations are noisy.** Lateral and longitudinal G computed from `v²/r` overestimate true values (real combined-G ≈ 1.8 g). The *shape* of the traces is reliable; the absolute magnitudes are not. Segers recommends dedicated accelerometers for accurate G measurement.
- **Vehicle parameters are estimates.** Cx, Cl and engine power are public approximations — real values are confidential team data.
- **Constant tyre friction (μ).** In reality μ varies with temperature, speed and wear (Pacejka model).
- **Drag coefficients are single-point estimates.** Each Cx is derived from one top-speed value, so the Monza↔Monaco comparison is qualitative (setup-level); a controlled coast-down test would be required for a precise cross-circuit measurement.
- **No suspension sensor data** is available through FastF1, so suspension analysis is kept theoretical.
## References
 
- Jorge Segers, *Analysis Techniques for Racecar Data Acquisition*, SAE International.
- FastF1 documentation — https://docs.fastf1.dev
---
 
**Author** — Edouard Bougeant · https://www.linkedin.com/in/edouard-bougeant-56bbb42a8/ · aspiring data & performance engineer in motorsport.