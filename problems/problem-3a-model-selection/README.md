# Model Selection for Linear Regression

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Statsmodels](https://img.shields.io/badge/Statsmodels-OLS-lightgrey)
![License](https://img.shields.io/badge/License-MIT-green)

A clean, reproducible model-selection workflow for choosing a parsimonious linear regression model using best-subset selection, information criteria, and stepwise procedures.

This project analyzes the assigned dataset `FE-GWP1_model_selection_1.csv` and selects the best regression model for predicting `Y` from five candidate predictors: `X1`, `X2`, `X3`, `X4`, and `X5`.

---

## Project Overview

The goal of this project is to avoid arbitrary trial-and-error model building by applying structured model-selection techniques. The notebook evaluates all candidate predictor subsets and compares the selected model against the full model using standard regression diagnostics and penalized fit criteria.

The final selected model is:

```text
Y ~ X2 + X3 + X4 + X5
```

This subset is supported consistently by multiple selection methods.

---

## Key Features

- Loads and validates the dataset structure
- Checks missing values and descriptive statistics
- Fits ordinary least squares regression models with `statsmodels`
- Performs exhaustive best-subset selection across all non-empty predictor combinations
- Evaluates candidate models using:
  - Adjusted R-squared
  - Akaike Information Criterion, AIC
  - Bayesian Information Criterion, BIC
- Runs forward selection using AIC
- Runs backward selection using BIC
- Compares the final selected model with the full five-predictor model
- Produces model-fit visualizations, including fitted versus actual values

---

## Repository Structure

```text
.
├── Problem_3a_model_selection.ipynb
├── Problem_3a_model_selection_enhanced.ipynb
├── FE-GWP1_model_selection_1.csv
└── README.md
```

### Main Notebook

`Problem_3a_model_selection_enhanced.ipynb` is the recommended version because it includes the full model-selection workflow, including backward selection and the final diagnostic plot.

---

## Dataset

The project uses a CSV file named:

```text
FE-GWP1_model_selection_1.csv
```

The dataset contains 100 observations and 6 columns:

| Variable | Description |
|---|---|
| `Y` | Response variable |
| `X1` | Candidate predictor |
| `X2` | Candidate predictor |
| `X3` | Candidate predictor |
| `X4` | Candidate predictor |
| `X5` | Candidate predictor |

The notebook confirms that there are no missing values in the dataset.

---

## Methodology

### 1. Best-Subset Selection

All possible non-empty combinations of the five candidate predictors are evaluated. Since there are five predictors, the exhaustive search compares:

```text
2^5 - 1 = 31 candidate models
```

Each model is ranked using adjusted R-squared, AIC, and BIC.

### 2. Forward Selection by AIC

Forward selection starts with an intercept-only model and adds predictors one at a time. At each step, the predictor that produces the largest AIC improvement is selected. The process stops when adding another variable no longer improves AIC.

### 3. Backward Selection by BIC

Backward selection starts with the full model and removes predictors one at a time. At each step, the predictor removal that gives the best BIC improvement is selected. The process stops when no further deletion improves BIC.

### 4. Final Model Comparison

The selected model is compared with the full model to verify whether the excluded predictor adds enough explanatory value to justify the additional complexity.

---

## Results

All three best-subset criteria selected the same model:

| Criterion | Selected Model | Value |
|---|---:|---:|
| Adjusted R-squared | `X2 + X3 + X4 + X5` | 0.633974 |
| AIC | `X2 + X3 + X4 + X5` | 260.616684 |
| BIC | `X2 + X3 + X4 + X5` | 273.642535 |

Forward AIC and backward BIC also selected the same final subset.

### Selected Model Performance

| Model | Predictors | Adjusted R-squared | AIC | BIC |
|---|---|---:|---:|---:|
| Selected model | `X2, X3, X4, X5` | 0.633974 | 260.616684 | 273.642535 |
| Full model | `X1, X2, X3, X4, X5` | 0.630170 | 262.592528 | 278.223549 |

The selected model outperforms the full model on adjusted R-squared, AIC, and BIC. This means `X1` does not add enough explanatory value to justify its inclusion.

---

## Final Regression Equation

The estimated final model is:

```text
Y = 1.1893 - 0.5861X2 + 0.5592X3 + 0.7105X4 - 0.1966X5
```

### Coefficient Summary

| Term | Coefficient | Std. Error | t-statistic | p-value |
|---|---:|---:|---:|---:|
| Intercept | 1.1893 | 0.0892 | 13.3331 | < 0.001 |
| `X2` | -0.5861 | 0.0910 | -6.4400 | < 0.001 |
| `X3` | 0.5592 | 0.0913 | 6.1240 | < 0.001 |
| `X4` | 0.7105 | 0.0819 | 8.6723 | < 0.001 |
| `X5` | -0.1966 | 0.0835 | -2.3551 | 0.0206 |

---

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/your-repository-name.git
cd your-repository-name
```

Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
python -m venv .venv
.venv\\Scripts\\activate
```

Install the required packages:

```bash
pip install pandas numpy matplotlib statsmodels jupyter
```

---

## Usage

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open the enhanced notebook:

```text
Problem_3a_model_selection_enhanced.ipynb
```

Run the cells from top to bottom. Make sure `FE-GWP1_model_selection_1.csv` is in the same directory as the notebook.

---

## Dependencies

This project uses:

- Python
- Jupyter Notebook
- pandas
- NumPy
- matplotlib
- statsmodels

---

## Interpretation

The project shows that the best predictive specification is not necessarily the largest model. Although the full model includes all five predictors, the selected four-predictor model performs better after accounting for model complexity.

The final model keeps `X2`, `X3`, `X4`, and `X5`, while excluding `X1`. This decision is supported by adjusted R-squared, AIC, BIC, forward selection, and backward selection.

---

## Reproducibility Notes

To reproduce the results exactly:

1. Keep the dataset filename as `FE-GWP1_model_selection_1.csv`.
2. Store the CSV file in the same directory as the notebook.
3. Run `Problem_3a_model_selection_enhanced.ipynb` from the first cell to the last cell.
4. Use the same Python package stack listed above.

---

## Future Improvements

Potential extensions include:

- Adding cross-validation for out-of-sample model assessment
- Testing residual assumptions more deeply
- Saving plots directly to an `outputs/` folder
- Adding a `requirements.txt` file
- Packaging the workflow as a reusable Python script

---

## Author

**Dossiya Dakou**

Project for model selection and regression analysis using Python.

---

## License

This project is available under the MIT License. Update this section if your repository uses a different license.
