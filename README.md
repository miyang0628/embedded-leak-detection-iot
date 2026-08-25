# Embedded Leak-Detection IoT — Reproducibility Repository

Reproducibility materials for the paper:

> **Embedding Leak-Detection IoT at the Design Stage: A Conceptual Framework
> for Shifting from Post-hoc Detection to Prevention in Buildings and Beyond**

This repository contains the complete code, parameter data, and generated
outputs for the illustrative cost–benefit simulation reported in the paper.
It allows full reproduction of every reported number, table, and figure from
a fixed random seed.

> **Note on anonymity.** This repository is shared for **double-blind peer
> review** and has been anonymized. It contains no author names, affiliations,
> or identifying metadata. Upon acceptance it will be replaced with a
> permanent, citable archive (with a DOI).

---

## What this analysis is (and is not)

The simulation is **illustrative, not confirmatory**. No primary field
measurements of embedded pipe-sensor performance exist yet, so the model
cannot prove that embedding is cheaper than retrofitting in any real
building. Its purpose is to:

1. demonstrate the **plausibility** of the design-stage prevention paradigm, and
2. locate the **decision boundary** — the sensor-coverage degradation rate at
   which the design-stage advantage disappears.

The headline output is therefore not "embedding wins" but a **break-even
degradation rate** and a **Monte Carlo probability** that make the
conclusion's dependence on the single unmeasured quantity (degradation rate
`ε`) explicit.

---

## Repository structure

```
.
├── README.md                        # this file
├── requirements.txt                 # Python dependencies
├── data/
│   └── parameters.csv               # all model inputs, with source + DOI
├── notebooks/
│   └── 01_cost_benefit_simulation.ipynb   # end-to-end analysis
└── results/
    ├── figures/
    │   ├── fig01_tco_comparison.{png,pdf}         # TCO by strategy
    │   ├── fig02_sensitivity_saving.{png,pdf}     # Monte Carlo distribution
    │   └── fig03_breakeven_degradation.{png,pdf}  # break-even on ε
    └── tables/
        ├── table01_tco_by_strategy.csv
        ├── table02_sensitivity_summary.csv
        └── table03_breakeven.csv
```

The paper's bibliography (`references.bib`) is also included at the repository
root for convenience.

---

## Requirements

- Python 3.10 or newer (developed and tested on 3.12)
- Packages listed in `requirements.txt`:

```
numpy
pandas
matplotlib
seaborn
```

Install with:

```bash
pip install -r requirements.txt
```

No GPU, network access, or proprietary software is required. The analysis
runs in seconds on a standard laptop.

---

## How to reproduce

1. Install the dependencies (above).
2. Open and run the notebook top to bottom:

```bash
jupyter notebook notebooks/01_cost_benefit_simulation.ipynb
```

or run it headless:

```bash
jupyter nbconvert --to notebook --execute \
  notebooks/01_cost_benefit_simulation.ipynb \
  --output 01_cost_benefit_simulation.ipynb
```

Running all cells regenerates every file under `results/` in place. A fixed
random seed (`numpy.random.default_rng(seed=42)`) guarantees that the
Monte Carlo results are bit-for-bit identical across runs.

---

## Mapping: paper ↔ repository

| Paper element | Produced by | Output file |
|---|---|---|
| Table (TCO by strategy) | Notebook Cell 4–5 | `results/tables/table01_tco_by_strategy.csv` |
| Table (Monte Carlo summary) | Notebook Cell 6 | `results/tables/table02_sensitivity_summary.csv` |
| Break-even value `ε*` | Notebook Cell 7 | `results/tables/table03_breakeven.csv` |
| Fig. (TCO comparison) | Notebook Cell 5 | `results/figures/fig01_tco_comparison.*` |
| Fig. (break-even on ε) | Notebook Cell 7 | `results/figures/fig03_breakeven_degradation.*` |
| Fig. (Monte Carlo saving) | Notebook Cell 8 | `results/figures/fig02_sensitivity_saving.*` |

Key reproduced values: discounted TCO of **\$3,833 / \$4,117 / \$5,032** for
embedded / retrofit / no-action; break-even degradation rate
**ε\* ≈ 6.3 %/yr**; probability that embedding is cheaper **≈ 0.51** across
10,000 Monte Carlo draws.

---

## The parameter table and its provenance

All model inputs live in `data/parameters.csv`, one row per parameter, each
with its value, unit, scope, source citation, DOI, and a note. Keeping the
citations in the data file (rather than hard-coded in the notebook) preserves
a full audit trail. Each parameter is classed by source quality:

- **Peer-reviewed / official (DOI available)** — e.g. global non-revenue
  water volume and cost; gastrointestinal-illness risk ratios;
  smart-meter efficacy. These carry a DOI in the `source_doi` column.
- **Industry / grey literature (no DOI)** — e.g. mean water-damage claim cost
  and frequency; automatic-shutoff loss-correlation figures. These are used
  only as **directional / upper-bound anchors**, never as sole quantitative
  evidence, and are flagged as such in the paper.
- **Modelling assumption** — e.g. sensor coverage factors, installation-cost
  ratio, and the **degradation rate `ε`**. These have no primary source and
  are the explicit objects of the break-even and Monte Carlo analyses.

> **Caveat on the effectiveness anchor.** The 96 % claim-frequency-reduction
> figure derives from an industry study of *whole-home shutoff devices*, a
> different device class from embedded pipe sensing. It is treated strictly
> as an optimistic upper bound and derated by coverage. See the paper's
> Limitations section.

> **Caveat on the degradation rate.** No field study has measured how fast
> un-serviceable embedded sensors lose coverage. The reported point value is
> a modelling assumption; the analysis is designed to expose the conclusion's
> sensitivity to it rather than to assert it.

---

## Method note: why the model is built to *not* pre-decide the result

An earlier formulation let the embedded strategy dominate on both installation
cost and effectiveness, which forced the Monte Carlo win-probability to 1.0 —
an artefact of the assumptions rather than a finding. The reported model
removes this by giving embedding a genuine structural disadvantage:
irreversibly enclosed sensors cannot be serviced, so their coverage **decays**
over the asset life, whereas accessible retrofit sensors are maintained and
stay flat. The winner is then determined by the degradation rate, not assumed,
which is what makes the break-even analysis meaningful.

---

## License

To be specified upon de-anonymization. During review, these materials are
provided solely for the purpose of peer evaluation.
