# Problem 1d - Omitted Variable Bias

## Scientific Overview

This project studies omitted-variable bias as an identification failure in linear regression. The econometric issue is not merely that the model is incomplete, but that exclusion of a relevant regressor changes the stochastic structure of the disturbance term. If the omitted variable is correlated with included regressors, the composite error becomes endogenous, violating the zero-conditional-mean assumption required for unbiased and consistent ordinary least squares estimation. :contentReference[oaicite:6]{index=6}

Formally, if the true model is

\[
Y_i = \beta_0 + \beta_1 X_i + \beta_2 W_i + \delta Z_i + \varepsilon_i,
\]

but the estimated model omits \( Z_i \), then the restricted disturbance becomes

\[
u_i = \delta Z_i + \varepsilon_i.
\]

If \( \operatorname{Cov}(X_i, Z_i) \neq 0 \), then

\[
E(u_i \mid X_i, W_i) \neq 0,
\]

and the slope estimator is biased because the included regressor partially proxies for the missing explanatory channel. This is the core mechanism of omitted-variable bias discussed in the report. :contentReference[oaicite:7]{index=7}

## Mathematical Identification Logic

The project emphasizes that the restricted-model coefficient does not estimate the same economic object as the full-model coefficient unless an orthogonality condition holds. In the benign special case where the omitted regressor is orthogonal to all included regressors, exclusion may reduce explanatory power but does not induce endogeneity in the restricted disturbance. Outside that case, coefficient interpretation changes fundamentally: the fitted slope conflates the direct effect of the included regressor with the indirect correlation structure induced by the omitted variable. :contentReference[oaicite:8]{index=8}

This can be summarized conceptually by the omitted-variable-bias decomposition:

\[
\plim \hat{\beta}_{X,\text{omitted}} = \beta_X + \text{Bias term},
\]

where the bias term depends on both the omitted effect \( \delta \) and the covariance structure between the omitted and included regressors. The report stresses that the sign and magnitude of the distortion are therefore determined jointly by economic relevance and dependence structure, not by sample size alone. :contentReference[oaicite:9]{index=9}

## Computational Design and Data-Science Workflow

The notebook demonstrates the theory through simulation. The true coefficient on \( X \) is set to 1.0, while the theoretical coefficient recovered by the omitted model is 1.6. The simulation then compares the full specification and the misspecified specification as sample size increases, which is a strong data-science design because it separates sampling variability from structural misspecification. 

In the full model, the estimated \( X \)-coefficient moves from 0.925568 at \( n = 200 \) to 1.002342 at \( n = 10{,}000 \), showing convergence to the true parameter. In the omitted model, the estimate moves from 1.481238 to 1.583250, converging toward the biased probability limit rather than the true coefficient. This is the central computational result: increasing data volume reduces variance but cannot correct systematic misspecification. 

## Statistical Interpretation

The simulation delivers a clean consistency argument. Under correct specification, the estimator concentrates around the true structural parameter. Under omission of a relevant correlated regressor, the estimator becomes consistent for the wrong estimand. This distinction is fundamental in financial engineering and econometrics because large datasets are common, yet large datasets do not rescue a structurally invalid model. 

## Financial Engineering Relevance

In financial applications, omitted-variable bias appears whenever a return, risk, spread, or price process is modeled without controlling for a latent but economically relevant driver. Examples include omitted market factors in asset pricing, omitted volatility or liquidity controls in execution models, and omitted macro state variables in forecasting equations. In all such cases, a coefficient that appears statistically stable may still be economically misleading because it is contaminated by missing state information. That is exactly why factor selection, feature justification, and model specification are central financial engineering tasks rather than cosmetic modeling choices. The report’s conclusion directly supports this interpretation: more data sharpen convergence toward the wrong parameter when the model is misspecified. 

## Evidence Summary

The report’s simulation evidence can be summarized as follows:

- True coefficient on \( X \): 1.000000
- Theoretical omitted-model coefficient on \( X \): 1.600000
- Estimated full-model coefficient at \( n = 200 \): 0.925568
- Estimated omitted-model coefficient at \( n = 200 \): 1.481238
- Estimated full-model coefficient at \( n = 10{,}000 \): 1.002342
- Estimated omitted-model coefficient at \( n = 10{,}000 \): 1.583250 

## Technical Deliverables in This Folder

- `notebook/` contains the simulation and estimation workflow.
- `html/` contains the polished mathematical presentation.
- `figures/` stores the convergence visualization.
- `results/` stores any numerical summaries or exported tables.

## Main Conclusion

This project shows that omitted-variable bias is a structural identification problem. The restricted regression is only valid under strict orthogonality conditions. Once a relevant correlated regressor is excluded, the error term becomes endogenous, the slope estimator is biased and inconsistent for the true structural coefficient, and larger samples merely improve precision around the wrong probability limit. 

## Author

**Dossiya Dakou**  
MSc Financial Engineering
