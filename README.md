# Posterior on the Baseline: Bayesian Tennis Tournament Predictions

## Project overview

This project implements a Bayesian Bradley–Terry (BT) pipeline for ATP tennis
matches, with static and dynamic models of player strength and optional
covariates, and compares them against a regularized frequentist BT baseline.

Each match is modeled as a Bernoulli event whose log-odds depend on the
difference in latent player skill; in the dynamic model, player skills evolve
over time via a random-walk prior over quarterly periods. This allows
us to capture gradual changes in form across seasons and to generate calibrated
probabilities for both individual matches and tournament outcomes via posterior
predictive simulation of the draw.

## Team

- Akshat Gupta
- Otto Miller
- Richard Liu

## Method summary

We implement several Bradley–Terry variants in PyMC:

- **Static BT**: Zero-sum baseline BT model with a single skill parameter per
  player.
- **Dynamic BT**: Time-varying skill via a random walk over quarter-periods,
  with per-period centering for identifiability.
- **Dynamic BT with covariates**: Adds pre-match covariates (surface, best-of,
  rank differences, age/height differences, etc.) on top of the dynamic latent
  skill.
- **Regularized BT MLE**: A ridge-penalized frequentist BT baseline for
  comparison.

Models are fitted with MCMC (NUTS) and, for the static case, with variational
inference (ADVI), and evaluated using log loss, Brier score, and calibration
curves on a strictly held-out future tournament (e.g. Wimbledon 2023).

## Data

### Primary source

We use real-world structured CSV match repositories from Jeff Sackmann’s open
ATP dataset:

- GitHub organisation:  
  https://github.com/JeffSackmann
- ATP match data repo:  
  https://github.com/JeffSackmann/tennis_atp

These yearly CSV files contain, for each match, winner/loser identifiers,
match dates, tournament metadata (name, level, surface), and basic statistics
such as rankings, ages, heights, and match duration.

The notebook expects yearly ATP match CSVs of the form:

- `atp_matches_2018.csv`
- …
- `atp_matches_2024.csv`

You can either:

- Download them manually from the `tennis_atp` repo into a local `data/`
  directory, or
- Use the notebook’s built-in HTTP loading, which reads directly from the raw
  GitHub URLs (no local download step required).

The dataset is **not** included in this repository for size and licensing
reasons; please obtain it from the original source above.

### Optional enrichment (not required to run)

Time permitting, this project can be extended with additional match-level
features from the Tennis Match Charting Project (for the subset of charted
matches), but this is treated as an optional enhancement rather than a core
dependency for the main results (static/dynamic BT and covariate models).

## How to run

1. Create and activate a Python environment, for example:

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # on Windows: .venv\Scripts\activate
