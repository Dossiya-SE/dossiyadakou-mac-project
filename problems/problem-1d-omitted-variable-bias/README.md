# Problem 1d - Omitted Variable Bias

## Overview

This problem examines **omitted variable bias (OVB)** in a regression model.

The purpose is to show that when a relevant variable is left out of the model, the estimated coefficient of an included regressor can become biased if the omitted variable both:
- affects the dependent variable, and
- is correlated with an included explanatory variable.

---

## Objective

The goal of this analysis is to:

1. explain why omitted variable bias occurs,
2. show how the bias affects coefficient estimates,
3. compare the biased model with the correctly specified model, and
4. interpret the implications for econometric analysis.

---

## Files

- `notebook/Problem_1d_omitted_variable_bias.ipynb`  
  Main notebook containing the full code and analysis.

- `html/Problem_1d_omitted_variable_bias_professional_math.html`  
  Exported HTML version for clean presentation.

- `figures/`  
  Plots and visual outputs related to the analysis.

- `results/`  
  Saved outputs, tables, or summary results.

---

## Method

The workflow for this problem is:

1. define the true data-generating process,
2. estimate a regression that omits a relevant explanatory variable,
3. compare the estimated coefficient with the true relationship,
4. analyze the direction and magnitude of the bias,
5. interpret the effect of the omitted variable on estimation results.

---

## Key Idea

Omitted variable bias arises when a variable that belongs in the model is excluded and is correlated with an included regressor. In that case, the included coefficient absorbs part of the omitted effect, leading to a biased estimate.

---

## Main Takeaway

This problem shows that increasing the sample size does **not** solve omitted variable bias. The issue is not randomness alone; it is a problem of model misspecification.

---

## How to Read This Folder

- Open the notebook for the full analysis.
- Open the HTML file for the presentation version.
- Check the figures and results folders for outputs.  
