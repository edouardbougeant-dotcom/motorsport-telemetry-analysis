# motorsport-telemetry-analysis
F1 telemetry analysis using Python — Vehicle dynamics, lap time simulation and data visualization

## Description
F1 telemetry analysis project — currently in active development.

## Author
I'm Edouard, a 21-year-old engineering student in my 3rd year.

## Motivation
This project was born from a desire to deepen my understanding of data and performance
engineering in motorsport. Beyond my academic curriculum, I dedicate my personal time
to acquiring hands-on experience with the tools, methodologies and workflows used by
performance engineers in professional racing environments.

## Technical Stack
- Python 3.12
- Jupyter Notebook
- pandas, numpy, matplotlib, FastF1

## Results

## Repo Structure
- `01_exploration_fastf1.ipynb` : Initial data ingestion and exploration using the FastF1
  API — first pass at telemetry parsing and time-series visualization.
- `02_lap_comparison_monaco_2023.ipynb` : Head-to-head lap delta analysis between the
  pole-sitter and P2 at Monaco 2023 — focused on identifying driving style differences
  through speed traces, brake points and throttle application profiles.

## How to use this project

**1. Clone the repo**
```bash
git clone https://github.com/edouardbougeant-dotcom/motorsport-telemetry-analysis.git
```

**2. Install dependencies**
```bash
pip install fastf1 matplotlib pandas numpy
```

**3. Launch Jupyter**
```bash
jupyter notebook
```