# Bayesian Tennis Bradley–Terry Pipeline

This repo contains a single Jupyter notebook implementing a Bayesian
Bradley–Terry pipeline for ATP tennis matches (static BT, dynamic BT,
covariates, and a ridge BT baseline). [file:170]

## Data

Source: Jeff Sackmann's ATP match data  
https://github.com/JeffSackmann/tennis_atp

The notebook expects yearly CSVs like:
- `atp_matches_2018.csv`
- ...
- `atp_matches_2024.csv`

You can either:
- Download them manually from the repo above into `data/`, or
- Let the notebook read directly from the raw GitHub URLs (already coded inside).

The dataset is NOT included in this repository for size and licensing reasons.

## How to run

1. Create a Python environment (e.g. `python -m venv .venv`).
2. Install dependencies:
   ```bash
   pip install numpy pandas pymc arviz matplotlib scipy scikit-learn
