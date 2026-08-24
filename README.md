# Embedded Leak-Detection IoT — Cost-Benefit Simulation

Replication code for the illustrative cost-benefit simulation in the paper
*"Embedding Leak-Detection IoT at the Design Stage: A Conceptual Framework
for Shifting from Post-hoc Detection to Prevention in Buildings and Beyond"*
(under review, anonymized for double-blind peer review).

> **Note.** Author, affiliation, and funding information are withheld in
> accordance with the double-blind review policy of the target venue.

## Overview

This repository reproduces the life-cycle cost (TCO) comparison and Monte
Carlo sensitivity analysis for three leak-detection strategies over an asset
life cycle: (a) no action, (b) post-hoc retrofit, and (c) design-stage
embedding. All results are illustrative, not confirmatory.

## Repository structure

```
embedded-leak-detection-iot/
├── data/
│   └── parameters.csv          # Model inputs with primary-source citations
├── notebooks/
│   └── 01_cost_benefit_simulation.ipynb
├── results/
│   ├── figures/                # Generated figures (PNG + PDF, 600 dpi)
│   └── tables/                 # Generated result tables (CSV)
├── requirements.txt
├── LICENSE
└── README.md
```

## Requirements

- Python 3.10+
- See `requirements.txt` (numpy, pandas, matplotlib, seaborn, jupyter)

```bash
pip install -r requirements.txt
```

## How to reproduce

1. Install dependencies (above).
2. Launch Jupyter and open `notebooks/01_cost_benefit_simulation.ipynb`.
3. Run all cells top to bottom.

Outputs are written to `results/figures/` (Fig. 1–2) and `results/tables/`
(Table 1–2). A fixed random seed (42) makes the Monte Carlo results
deterministic across runs.

## Data and provenance

Every numeric input is stored in `data/parameters.csv` together with its
unit, scope, and primary-source citation (author, venue, DOI where
available). No proprietary or restricted data are used; all inputs derive
from published literature and public statistics.

## Citation

Citation details are withheld during the anonymized review period and will
be added upon acceptance.

## License

Released under the MIT License. See `LICENSE`.
