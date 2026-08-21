# Financial Engineering Models — Econometrics, Time Series and Model Risk

<p align="center"><img src="assets/math-art/econometric-risk-atlas.svg" width="100%" alt="Econometric model risk atlas" /></p>

The repository is organized around five quantitative failure modes: **identification error, influential observations, over/under-specification, nonstationarity and structural instability**.

## Problem map

| Module | Mathematical object | Evidence type |
|---|---|---|
| [Omitted Variable Bias](problems/problem-1d-omitted-variable-bias/README.md) | `plim β̂omit = β + γ Cov(X,Z)/Var(X)` | analytical + seeded synthetic |
| [Outlier Sensitivity](problems/problem-2b-outlier-sensitivity/README.md) | leverage / influence geometry | diagnostic + robustness |
| [Model Selection](problems/problem-3a-model-selection/README.md) | likelihood–complexity trade-off | comparative specification |
| [Stationarity / Unit Root](problems/problem-5-stationarity-unit-root/README.md) | stochastic persistence / ADF-type structure | time-series diagnostic |
| [Structural Break](problems/problem-6a-structural-break/README.md) | parameter regime `β₁ → β₂` at break `τ` | stability diagnostic |

## Repository rule

```text
estimand → assumptions → analytical target → computation → diagnostic → sensitivity → model-risk boundary
```

A simulation is not market evidence. A good in-sample fit is not model validity. A stable point estimate without sensitivity analysis is not treated as complete evidence.

## Cross-language role

**Python** — primary numerical/statistical implementation.  
**R / Julia** — independent formulation or translation where a module includes it.  
**SQL** — explicit result/data schema examples.

Language examples are not used as proficiency inflation.

## Reproducibility gate

Each mature problem should expose source/data, variable definitions, deterministic seed when applicable, estimator/test, generated results, diagnostics and limitations.

```text
problem/
├── README.md
├── notebook/
├── code/
├── figures/
├── output/
└── data/ or source note
```

## Interpretation boundary

This repository demonstrates quantitative model reasoning and model-risk analysis. It does **not** establish trading profitability, universal causal identification, production-grade risk infrastructure or robustness across every market regime.

[Group report](reports/Group_report.docx) · [Research portfolio](https://dossiya-se.github.io/)
