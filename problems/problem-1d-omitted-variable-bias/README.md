# Problem 1d — Omitted Variable Bias

## Overview

This project studies **omitted variable bias** as an identification problem in linear regression. The issue is not simply that a regression model is incomplete. The deeper problem is that omitting a relevant variable changes the structure of the regression error term.

When the omitted variable is correlated with one or more included regressors, the restricted model violates the zero conditional mean assumption required for unbiased and consistent ordinary least squares estimation. In that case, the estimated coefficient no longer recovers the intended structural parameter.

---

## Econometric Framework

Suppose the true data-generating process is

$$
Y_i = \beta_0 + \beta_1 X_i + \beta_2 W_i + \delta Z_i + \varepsilon_i,
$$

where \(Z_i\) is a relevant explanatory variable.

If \(Z_i\) is omitted, the estimated restricted model becomes

$$
Y_i = \alpha_0 + \alpha_1 X_i + \alpha_2 W_i + u_i,
$$

where the restricted disturbance is

$$
u_i = \delta Z_i + \varepsilon_i.
$$

The omitted variable is now embedded in the error term. If

$$
\operatorname{Cov}(X_i, Z_i) \neq 0,
$$

then the composite error term is correlated with the included regressor, so

$$
E(u_i \mid X_i, W_i) \neq 0.
$$

This violates the exogeneity condition for OLS. As a result, the restricted-model coefficient on \(X_i\) absorbs part of the missing explanatory channel carried by \(Z_i\).

---

## Identification Logic

The coefficient from the restricted model does not generally estimate the same object as the coefficient from the correctly specified model.

The full model coefficient \(\beta_1\) measures the partial effect of \(X_i\) on \(Y_i\), holding both \(W_i\) and \(Z_i\) fixed. By contrast, the restricted-model coefficient reflects the effect of \(X_i\) plus the component of \(Z_i\) that is statistically associated with \(X_i\).

Conceptually,

$$
\operatorname{plim}\hat{\alpha}_1
=
\beta_1
+
\text{Bias term}.
$$

The bias term depends on two elements:

1. The causal or structural importance of the omitted variable, represented by \(\delta\)
2. The dependence structure between the omitted variable and the included regressors

Therefore, the direction and size of omitted variable bias are determined jointly by **economic relevance** and **correlation structure**. Increasing the sample size reduces sampling variability, but it does not eliminate structural misspecification.

---

## Computational Design

The notebook demonstrates the theory using a controlled simulation.

The simulation is designed so that:

- The true coefficient on \(X\) is \(1.0\)
- The theoretical probability limit of the omitted-variable estimator is \(1.6\)
- The full model includes the relevant regressor
- The restricted model omits the relevant correlated regressor
- Sample size is increased to distinguish sampling noise from structural bias

This design makes the identification failure visible. If the estimator is correctly specified, it should converge toward the true coefficient. If the model is misspecified, it should converge toward the biased probability limit.

---

## Simulation Results

| Model | Sample Size | Estimated Coefficient on \(X\) | Target of Convergence |
|---|---:|---:|---:|
| Full model | 200 | 0.925568 | True coefficient: 1.000000 |
| Omitted-variable model | 200 | 1.481238 | Biased probability limit: 1.600000 |
| Full model | 10,000 | 1.002342 | True coefficient: 1.000000 |
| Omitted-variable model | 10,000 | 1.583250 | Biased probability limit: 1.600000 |

The full model converges toward the true structural coefficient. The omitted-variable model converges toward the wrong estimand.

This is the key computational result: **more data reduce variance, but they do not correct bias caused by misspecification.**

---

## Statistical Interpretation

The simulation highlights the difference between precision and validity.

Under correct specification, the OLS estimator concentrates around the true parameter as the sample size increases. Under omitted variable bias, the estimator may also become more stable, but it stabilizes around the wrong value.

This distinction matters in modern empirical work because large datasets can create a false sense of reliability. A coefficient can appear precise, stable, and statistically significant while still being economically invalid if the model omits a relevant correlated driver.

---

## Financial Engineering Relevance

Omitted variable bias is especially important in financial engineering because financial data often contain latent or partially observed state variables.

Examples include:

- Asset-pricing models that omit relevant risk factors
- Return models that omit volatility, liquidity, or macroeconomic controls
- Credit-spread models that omit borrower, market, or business-cycle conditions
- Execution models that omit market depth or order-flow information
- Forecasting models that omit regime variables or hidden state dynamics

In these settings, a coefficient may look statistically strong but still reflect a contaminated relationship. The model may be estimating a mixture of direct effects and omitted state-variable effects.

For this reason, factor selection, feature justification, diagnostics, and specification testing are central financial engineering tasks. They are not cosmetic modeling choices.

---

## Technical Deliverables

```text
problem-1d/
├── notebook/     # Simulation and estimation workflow
├── html/         # Polished mathematical presentation
├── figures/      # Convergence visualizations
└── results/      # Numerical summaries and exported tables
