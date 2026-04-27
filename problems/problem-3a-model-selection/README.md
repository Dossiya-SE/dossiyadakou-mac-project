# Research-Driven Model Selection for Linear Regression

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Statsmodels](https://img.shields.io/badge/Statsmodels-OLS-lightgrey)
![Model Selection](https://img.shields.io/badge/Method-Best%20Subset%20%7C%20AIC%20%7C%20BIC-purple)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

A research-style statistical modeling project that applies **structured model selection** to identify a parsimonious linear regression model for predicting `Y` from five candidate predictors: `X1`, `X2`, `X3`, `X4`, and `X5`.

The project goes beyond fitting a single regression model. It demonstrates a complete analytical workflow: data validation, candidate model construction, exhaustive subset search, information-criterion comparison, stepwise selection, model benchmarking, coefficient interpretation, and visual diagnostics.

---

## Executive Summary

The objective is to select a regression model that balances **explanatory strength** with **model simplicity**. Instead of keeping all predictors by default, the notebook evaluates whether each variable improves the model enough to justify its complexity.

After comparing all non-empty predictor subsets and validating the result with forward and backward selection procedures, the recommended model is:

```text
Y ~ X2 + X3 + X4 + X5
```

This model is preferred over the full five-predictor model because it achieves:

- higher adjusted R-squared,
- lower Akaike Information Criterion, AIC,
- lower Bayesian Information Criterion, BIC,
- agreement across multiple model-selection strategies,
- a more parsimonious specification that excludes `X1`.

---

## Research Skills Demonstrated

| Research / Analytical Skill | Evidence in This Project |
|---|---|
| Problem formulation | Defines a clear supervised modeling question: predict `Y` using candidate regressors `X1` through `X5`. |
| Data validation | Checks dataset dimensions, column structure, descriptive statistics, and missing values before modeling. |
| Statistical modeling | Fits ordinary least squares, OLS, regression models using `statsmodels`. |
| Exhaustive model comparison | Evaluates all `2^5 - 1 = 31` non-empty predictor subsets. |
| Objective selection criteria | Compares models using adjusted R-squared, AIC, and BIC rather than subjective trial-and-error. |
| Parsimony reasoning | Selects the simpler model when the full model does not improve penalized fit. |
| Algorithmic selection | Implements forward selection using AIC and backward selection using BIC. |
| Model benchmarking | Compares the final selected model directly against the full model. |
| Statistical inference | Reports coefficient estimates, standard errors, t-statistics, p-values, and confidence intervals. |
| Diagnostic communication | Includes fitted-versus-actual visualization and interprets the model in practical terms. |
| Reproducible analysis | Uses a notebook-based workflow with clear code, deterministic subset enumeration, and documented execution steps. |

---

## Repository Contents

```text
.
├── Problem_3a_model_selection.ipynb              # Original model-selection notebook
├── Problem_3a_model_selection_enhanced.ipynb     # Recommended enhanced notebook
├── FE-GWP1_model_selection_1.csv                 # Input dataset expected by the notebook
└── README.md                                     # Project documentation
```

### Recommended Notebook

Use:

```text
Problem_3a_model_selection_enhanced.ipynb
```

This version contains the most complete workflow, including data checks, exhaustive best-subset selection, forward AIC selection, backward BIC selection, final model comparison, coefficient reporting, and fitted-versus-actual visualization.

---

## Dataset

The analysis uses the assigned dataset:

```text
FE-GWP1_model_selection_1.csv
```

The notebook validates the following structure:

| Property | Value |
|---|---:|
| Observations | 100 |
| Columns | 6 |
| Response variable | `Y` |
| Candidate predictors | `X1`, `X2`, `X3`, `X4`, `X5` |
| Missing values | 0 |

### Variable Dictionary

| Variable | Role | Description |
|---|---|---|
| `Y` | Response | Outcome variable to be predicted. |
| `X1` | Candidate predictor | Evaluated for inclusion in the regression model. |
| `X2` | Candidate predictor | Evaluated for inclusion in the regression model. |
| `X3` | Candidate predictor | Evaluated for inclusion in the regression model. |
| `X4` | Candidate predictor | Evaluated for inclusion in the regression model. |
| `X5` | Candidate predictor | Evaluated for inclusion in the regression model. |

The predictors are anonymized, so the project focuses on rigorous model-selection methodology rather than domain-specific causal interpretation.

---

## Methodology

The workflow follows a research-oriented modeling sequence:

```text
Data audit
   -> Model specification
   -> Exhaustive subset search
   -> Criterion-based ranking
   -> Forward and backward selection checks
   -> Final model comparison
   -> Coefficient interpretation
   -> Diagnostic visualization
```

### 1. Data Audit

Before fitting models, the notebook verifies:

- dataset shape,
- expected column names,
- missing-value counts,
- summary statistics for each variable.

This prevents downstream modeling errors and confirms that the analytical assumptions are based on the actual dataset structure.

### 2. Candidate Model Space

The full candidate specification is:

```text
Y = beta_0 + beta_1 X1 + beta_2 X2 + beta_3 X3 + beta_4 X4 + beta_5 X5 + error
```

Since there are five candidate predictors, the exhaustive search evaluates:

```text
2^5 - 1 = 31 candidate models
```

The intercept-only model is used as the starting point for forward selection, but the ranked subset table focuses on all non-empty predictor combinations.

### 3. Best-Subset Selection

Every non-empty subset of `X1` through `X5` is fitted using OLS. Each model is scored using:

| Criterion | Optimization Direction | Purpose |
|---|---|---|
| Adjusted R-squared | Higher is better | Rewards explanatory power while penalizing unnecessary predictors. |
| AIC | Lower is better | Balances fit and complexity, with a lighter penalty than BIC. |
| BIC | Lower is better | Applies a stronger complexity penalty, often favoring simpler models. |

### 4. Forward Selection by AIC

Forward selection starts from an intercept-only model and adds the predictor that most improves AIC at each step. The selected path is:

```text
X4 -> X3 -> X2 -> X5
```

The final forward-selected model contains the same predictor set as the best-subset result:

```text
X2 + X3 + X4 + X5
```

### 5. Backward Selection by BIC

Backward selection starts from the full model and removes predictors when doing so improves BIC. The procedure removes:

```text
X1
```

The resulting model is again:

```text
X2 + X3 + X4 + X5
```

### 6. Final Model Benchmarking

The selected model is benchmarked against the full five-predictor model to test whether excluding `X1` improves parsimony without sacrificing model quality.

---

## Results

### Best Model by Selection Criterion

All three primary subset-selection criteria identify the same model.

| Criterion | Selected Model | Value |
|---|---|---:|
| Adjusted R-squared | `X2 + X3 + X4 + X5` | 0.633974 |
| AIC | `X2 + X3 + X4 + X5` | 260.616684 |
| BIC | `X2 + X3 + X4 + X5` | 273.642535 |

### Best Model at Each Size

| Number of Predictors | Best Predictor Set | Adjusted R-squared | AIC | BIC |
|---:|---|---:|---:|---:|
| 1 | `X4` | 0.282529 | 325.028687 | 330.239028 |
| 2 | `X3 + X4` | 0.466143 | 296.442510 | 304.258021 |
| 3 | `X2 + X3 + X4` | 0.616639 | 264.291054 | 274.711735 |
| 4 | `X2 + X3 + X4 + X5` | 0.633974 | 260.616684 | 273.642535 |
| 5 | `X1 + X2 + X3 + X4 + X5` | 0.630170 | 262.592528 | 278.223549 |

The four-predictor model improves on the three-predictor model. Adding `X1` to create the full model slightly increases raw R-squared but worsens adjusted R-squared, AIC, and BIC.

### Selected Model vs. Full Model

| Model | Predictors | Adjusted R-squared | AIC | BIC |
|---|---|---:|---:|---:|
| Selected model | `X2, X3, X4, X5` | 0.633974 | 260.616684 | 273.642535 |
| Full model | `X1, X2, X3, X4, X5` | 0.630170 | 262.592528 | 278.223549 |

The selected model is preferred because it is simpler and performs better under all three reported penalized or complexity-aware criteria.

---

## Final Regression Model

The estimated final equation is:

```text
Y = 1.1893 - 0.5861*X2 + 0.5592*X3 + 0.7105*X4 - 0.1966*X5
```

### Coefficient Summary

| Term | Coefficient | Std. Error | t-statistic | p-value | 95% CI Lower | 95% CI Upper |
|---|---:|---:|---:|---:|---:|---:|
| Intercept | 1.189339 | 0.089202 | 13.333088 | < 0.001 | 1.012251 | 1.366428 |
| `X2` | -0.586083 | 0.091007 | -6.440013 | < 0.001 | -0.766754 | -0.405412 |
| `X3` | 0.559157 | 0.091306 | 6.123977 | < 0.001 | 0.377891 | 0.740423 |
| `X4` | 0.710541 | 0.081932 | 8.672333 | < 0.001 | 0.547885 | 0.873196 |
| `X5` | -0.196639 | 0.083495 | -2.355107 | 0.020574 | -0.362398 | -0.030881 |

### Model Fit Statistics

| Statistic | Value |
|---|---:|
| R-squared | 0.648763 |
| Adjusted R-squared | 0.633974 |
| F-statistic | 43.87 |
| Prob. F-statistic | 8.29e-21 |
| AIC | 260.616684 |
| BIC | 273.642535 |
| Number of observations | 100 |
| Residual degrees of freedom | 95 |

---

## Interpretation

The selected model indicates that, conditional on the other included predictors:

- `X4` has the strongest positive association with `Y` among the selected variables.
- `X3` is also positively associated with `Y`.
- `X2` is negatively associated with `Y`.
- `X5` is negatively associated with `Y`, with a smaller magnitude than `X2`.
- `X1` is excluded because it does not improve the model enough after accounting for complexity.

Because the variables are anonymized and the analysis is observational, the coefficient estimates should be interpreted as statistical associations, not causal effects.

---

## Why This Model Is Research-Defensible

The final model is not chosen from a single metric or a subjective preference. It is supported by multiple independent checks:

| Validation Check | Result |
|---|---|
| Exhaustive best subset by adjusted R-squared | Selects `X2 + X3 + X4 + X5` |
| Exhaustive best subset by AIC | Selects `X2 + X3 + X4 + X5` |
| Exhaustive best subset by BIC | Selects `X2 + X3 + X4 + X5` |
| Forward selection by AIC | Selects `X4 + X3 + X2 + X5` |
| Backward selection by BIC | Removes `X1`, leaving `X2 + X3 + X4 + X5` |
| Full-model comparison | Selected model has better adjusted R-squared, AIC, and BIC |

This agreement strengthens confidence that the selected model is not an artifact of one specific selection rule.

---

## Reproducibility

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repository-name.git
cd your-repository-name
```

### 2. Create a Virtual Environment

macOS / Linux:

```bash
python -m venv .venv
source .venv/bin/activate
```

Windows PowerShell:

```bash
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install Dependencies

```bash
pip install pandas numpy matplotlib statsmodels jupyter
```

Optional: create a `requirements.txt` file for cleaner setup:

```text
pandas
numpy
matplotlib
statsmodels
jupyter
```

Then install with:

```bash
pip install -r requirements.txt
```

### 4. Run the Notebook

```bash
jupyter notebook
```

Open and run:

```text
Problem_3a_model_selection_enhanced.ipynb
```

Ensure that the dataset file is located in the same directory as the notebook:

```text
FE-GWP1_model_selection_1.csv
```

---

## Technical Stack

| Tool | Purpose |
|---|---|
| Python | Core programming language |
| Jupyter Notebook | Literate analysis and reproducible workflow |
| pandas | Data loading, validation, and tabular reporting |
| NumPy | Numerical operations |
| statsmodels | OLS regression and model statistics |
| matplotlib | Model-selection and diagnostic visualization |
| itertools | Exhaustive subset generation |

---

## Suggested Repository Enhancements

For a production-quality GitHub repository, consider adding:

```text
requirements.txt
.gitignore
LICENSE
outputs/
figures/
src/
```

Recommended next improvements:

- save all model-selection tables to `outputs/`,
- export diagnostic plots to `figures/`,
- add residual plots and Q-Q plots,
- include cross-validation for out-of-sample validation,
- compare OLS selection with regularized regression methods such as Ridge, Lasso, or Elastic Net,
- convert reusable functions into a Python module under `src/`,
- add a short methods note explaining AIC and BIC for non-technical readers.

---

## Limitations

This project is intentionally focused on model selection using in-sample OLS criteria. The current notebook does not yet include:

- train-test split validation,
- k-fold cross-validation,
- residual normality plots beyond the reported summary statistics,
- heteroskedasticity tests,
- influence diagnostics such as Cook's distance,
- domain interpretation of anonymized predictors.

These limitations do not invalidate the selected model, but they define the scope of the current analysis and provide a clear path for future research extensions.

---

## Key Takeaway

The analysis shows that the best model is not necessarily the largest model. The four-predictor specification using `X2`, `X3`, `X4`, and `X5` offers a better balance of fit and parsimony than the full model that also includes `X1`.

The final recommendation is:

```text
Use Y ~ X2 + X3 + X4 + X5 as the selected OLS model.
```

---

## Author

**Dossiya Dakou**

Statistical modeling project demonstrating regression analysis, model selection, and research-style quantitative reasoning in Python.

---

## License

This project is available under the MIT License. Update this section if your repository uses a different license.
