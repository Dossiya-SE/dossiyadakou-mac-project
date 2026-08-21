# Financial Engineering Models — Econometrics, Time Series and Model Risk

This repository contains MSc Financial Engineering computational work organized as **problem-level evidence packages** rather than a single undifferentiated notebook archive.

Each problem is intended to connect:

```text
question
→ mathematical/statistical formulation
→ assumptions
→ computational experiment
→ diagnostics
→ interpretation
→ limitations
```

The repository is educational/research work. It is **not** a production trading system, investment recommendation, or claim of predictive profitability.

## Current problem set

| Problem | Main question | Mathematical / statistical focus |
|---|---|---|
| [Problem 1d — Omitted Variable Bias](problems/problem-1d-omitted-variable-bias/README.md) | What happens to an OLS coefficient when a relevant correlated regressor is omitted? | identification, OLS probability limits, model misspecification |
| [Problem 2b — Outlier Sensitivity](problems/problem-2b-outlier-sensitivity/README.md) | How sensitive are estimates/inference to influential observations? | robustness, influence, estimator sensitivity |
| [Problem 3a — Model Selection](problems/problem-3a-model-selection/README.md) | How should competing specifications be compared without confusing fit with validity? | specification comparison, diagnostics, model risk |
| [Problem 5 — Stationarity / Unit Root](problems/problem-5-stationarity-unit-root/README.md) | Is a time series statistically compatible with stationarity or unit-root behavior? | stochastic processes, time-series diagnostics, unit-root testing |
| [Problem 6a — Structural Break](problems/problem-6a-structural-break/README.md) | Does a stable parameter model remain defensible across a regime change? | parameter instability, structural breaks, regime sensitivity |

## Example of evidence depth

The omitted-variable-bias module does not stop at reporting a regression coefficient. It specifies a known data-generating process,

```math
Y_i=a+bX_i+cZ_i+e_i,
```

constructs correlation between `X` and the omitted regressor `Z`, derives the probability-limit target,

```math
\operatorname{plim}\hat\beta_{omit}
=
b+c\frac{\operatorname{Cov}(X,Z)}{\operatorname{Var}(X)},
```

and then compares finite- and large-sample simulations with that analytical result.

That structure is the repository standard: **theory gives a falsifiable computational target; code is checked against the target; interpretation remains conditional on assumptions.**

## Evidence classes used in this repository

- **Analytical result** — derived from the declared statistical model.
- **Synthetic experiment** — generated from a known data-generating process.
- **Empirical result** — computed from a supplied dataset, when applicable.
- **Diagnostic result** — test statistic, residual diagnostic, influence measure or specification comparison.
- **Interpretation** — conclusion conditional on the model assumptions and diagnostics.
- **Limitation** — known reason the conclusion may not generalize.

A synthetic simulation is never described as market evidence.

## Model-risk discipline

A numerical result is not accepted at face value. The intended review questions are:

1. **Estimand:** what quantity is the model actually estimating?
2. **Identification:** under what assumptions does the estimator correspond to that quantity?
3. **Specification:** what relevant structure may be missing?
4. **Sampling:** how much of the result is finite-sample variation?
5. **Diagnostics:** what do residuals, influence measures or time-series tests reveal?
6. **Stability:** does the result survive outliers, sample changes or structural breaks?
7. **Uncertainty:** what interval, distribution or sensitivity range accompanies the point estimate?
8. **Decision boundary:** what conclusion would change if assumptions fail?

## Reproducibility standard

A strong problem folder should contain, where applicable:

```text
problem/
├── README.md          # formulation, derivation, results, interpretation
├── notebook/          # executable analysis
├── code/              # reusable scripts/functions
├── figures/           # generated visual evidence
├── output/            # machine-readable results
└── data/ or source note
```

Existing problem folders are at different maturity levels; the README of each folder is the authoritative statement of what is actually present.

## Cross-language validation

Some problem documentation includes equivalent or validation-oriented examples in Python, R, Julia or SQL. These serve distinct purposes:

- **Python** — primary numerical/statistical implementation;
- **R** — independent statistical formulation where useful;
- **Julia** — numerical/modeling translation where useful;
- **SQL** — explicit result/data schema examples.

The presence of an example in a language is **not** presented as equal expert proficiency in every language.

## Quality requirements for numerical claims

Before a result is treated as evidence, the preferred chain is:

```text
data-generating process / source
→ variable definitions
→ assumptions
→ estimator / test
→ code
→ deterministic seed where simulation is used
→ diagnostics
→ sensitivity / robustness
→ interpretation
```

For Monte Carlo or simulation work, seeds and sample sizes should be declared. For time-series work, the ordering, frequency, transformations and test assumptions should be explicit.

## Repository structure

```text
.
├── README.md
├── docs/                 # general documentation
├── reports/              # written group/project reports
└── problems/             # one folder per problem
    ├── problem-1d-omitted-variable-bias/
    ├── problem-2b-outlier-sensitivity/
    ├── problem-3a-model-selection/
    ├── problem-5-stationarity-unit-root/
    └── problem-6a-structural-break/
```

## What this repository demonstrates

The public evidence supports competence in:

- translating statistical questions into explicit estimands and assumptions;
- deriving and checking model behavior rather than relying only on library output;
- separating sampling error from structural misspecification;
- treating outliers and model choice as model-risk questions;
- applying stationarity/unit-root and structural-break reasoning to time-series problems;
- documenting computations so the mathematical interpretation remains inspectable.

## What it does not establish

This repository does **not** by itself establish:

- profitable trading performance;
- causal identification in real financial markets unless separately justified;
- production-grade risk infrastructure;
- robustness to every market regime;
- independent replication outside the repository.

Those require additional data, validation, backtesting controls, transaction-cost modeling, out-of-sample evaluation and governance.

## Reports

- [Group report](reports/Group_report.docx)

## Author

**Dossiya Dakou**

Research portfolio: https://dossiya-se.github.io/
