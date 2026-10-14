# Particle-Decay Parameter Inference with Pseudoexperiments

**Saqib Umair**  
MSc Particle and Nuclear Physics, University of Edinburgh

This project uses Monte Carlo pseudoexperiments and unbinned maximum-likelihood fits to study how background contamination affects parameter estimation in a simulated oscillating particle-decay model.

The parameters of interest are the lifetime `tau`, oscillation frequency `Delta m`, and modulation parameter `V`.

## Why this project matters

A fit can look statistically precise and still be wrong if the likelihood does not describe the data-generating process. This project tests that directly by comparing:

- a **signal-only likelihood** applied to contaminated samples;
- a **signal + background likelihood** that includes the nuisance component explicitly.

Background fractions of **1%, 10%, and 20%** are studied with repeated pseudoexperiments.

## Model

The signal model is

`p_sig(t) proportional to [1 + V sin(Delta m t)] exp(-t/tau)`

over a finite decay-time interval.

The background component is represented by a truncated Gaussian in decay time. Both PDFs are normalised numerically over the accepted range.

Events are generated with accept-reject sampling and fitted with an unbinned negative log-likelihood using `iminuit`.

## Main result

At **20% background contamination**, the saved ensemble gives:

| Parameter | Generated value | Signal-only mean | Signal + background mean |
|---|---:|---:|---:|
| `tau` | 1.50e-6 s | 1.24e-6 s | 1.50e-6 s |
| `V` | 0.100 | 0.0545 | 0.101 |

Ignoring the background produces a large shift in both fitted quantities. Once the background component is included in the likelihood, the fitted means return close to the generated values.

This is the central result of the project: **likelihood misspecification can produce a bias much larger than the statistical spread of the fit.**

## Background study

![Lifetime fit comparison](figures/background_tau_comparison.jpg)

![Modulation-parameter fit comparison](figures/background_V_comparison.jpg)

## Baseline pseudoexperiments

A pure-signal ensemble is used first to examine the fitted-parameter distributions before background is introduced.

![Generated signal sample](figures/generated_signal_sample.jpg)

The saved baseline ensemble shows good closure for `tau` and `Delta m`, while `V` shows a visible positive offset. I retain that feature in the public version rather than presenting the baseline as an ideal closure test.

## Methods demonstrated

- Monte Carlo accept-reject sampling
- numerical PDF normalisation
- unbinned maximum-likelihood estimation
- pseudoexperiment ensembles
- bias and precision estimation
- nuisance/background modelling
- comparison of correctly specified and misspecified likelihoods

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── decay_parameter_pseudoexperiments.ipynb
├── figures/
│   ├── generated_signal_sample.jpg
│   ├── background_tau_comparison.jpg
│   └── background_V_comparison.jpg
└── results/
    └── background_fit_summary.csv
```

## Reproducibility

The public notebook contains the full analysis code with outputs cleared to keep the repository compact. Numerical values and figures are taken from the saved coursework run.

The original analysis did not fix a random seed, so repeated executions can produce small changes in ensemble means and fitted biases.

Install the dependencies with:

```bash
pip install -r requirements.txt
```

## Tools

Python · NumPy · SciPy · pandas · Matplotlib · iminuit
