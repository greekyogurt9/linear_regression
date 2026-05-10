# Linear Regression Checklist

An end-to-end, actionable checklist for building linear regression models — from problem framing through communication of results. Covers both prediction and inference tasks.

## Overview

This interactive checklist guides you through the complete linear regression workflow. It works for any continuous outcome variable where observations are independent and relationships are approximately linear.

### When to Use This Checklist

✓ **Predicting** a continuous outcome (revenue, price, temperature)  
✓ **Understanding** which variables drive a continuous outcome  
✓ **Both** prediction and inference tasks  

### When NOT to Use This Checklist

✗ Count data (number of visits, claims) → use Poisson or negative binomial regression  
✗ Ordinal outcomes (ratings 1–5, satisfaction levels) → use ordered logistic regression  
✗ Binary outcomes (yes/no, default/no-default) → use logistic regression  
✗ Time series data → use ARIMA, state-space models, or time series regression  
✗ Hierarchical data (repeated measurements, nested clusters) → use mixed-effects models  
✗ Highly nonlinear relationships → use GAM, splines, or machine learning methods  

## Workflow Phases

The checklist is organized into 10 interconnected phases:

### **01. Frame the Problem** — Before opening any data
- Define Y precisely (not "customer value" but "total spend in next 90 days")
- Decide: Prediction or Inference?
- List candidate X variables using business intuition
- Understand your outcome type and choose the right method

### **02. Exploratory Data Analysis (Full Dataset)** — Understand structure without preprocessing
- Explore distributions of all variables
- Scatter plot each X against Y for linearity and outliers
- Check pairwise correlations between predictors
- Identify candidate interaction effects
- *Critical*: Do NOT make preprocessing decisions on full data (data leakage)

### **03. Train/Test Split** — Isolate future test performance
- Split data into training and test sets (typically 70/30 or 80/20)
- Use stratified sampling if imbalanced
- Random seed for reproducibility

### **04. Preprocessing (on Training Data Only)**
- Handle missing values (on training set, apply same rules to test)
- Transform Y if heavily skewed (log, Box-Cox, square root)
- Transform X variables (polynomial terms, log, square root)
- Encode categorical variables
- Scale/normalize if needed
- Select variables based on training set correlations

### **05. Assumptions You Can Check Before Fitting**
- **Linearity**: Do scatter plots suggest straight-line relationships?
- **Independence**: Are observations independent? (no time-series structure, no clustering)
- **No perfect multicollinearity**: Xs must not be exact linear combinations

### **06. Establish Baselines**
- Fit the null model (predict mean of Y for all observations)
- Fit simple regression on your strongest single predictor
- Use these as reference points for improvement

### **07. Build the Full Model**
- Fit linear regression with all candidate variables
- Record coefficients, standard errors, p-values, confidence intervals
- Compute R², RMSE, AIC, BIC on training set

### **08. Variable Selection** — Remove noise, keep signal
- Use backward elimination, forward selection, or stepwise methods (AIC/BIC)
- Alternative: Regularization (Ridge, Lasso, Elastic Net) for prediction
- Refit smaller model and compare to null and simple baselines
- Trade-off: fewer variables (interpretability) vs. fit improvement

### **09. Diagnostic Checks (Post-Fit Residual Analysis)**
- Residuals vs. fitted values (check homoscedasticity and linearity)
- Q-Q plot (check normality of errors)
- Scale-Location plot (confirm constant variance)
- Residuals vs. leverage (identify influential outliers via Cook's distance)
- Check for correlated errors (autocorrelation if applicable)
- Assess multicollinearity via VIF (Variance Inflation Factor)

### **10. Communication & Deployment**
- **For Prediction**: Report test set RMSE, MAE, mean absolute percent error
- **For Inference**: Report coefficients with 95% CIs, p-values, interpretations
- Document assumptions, limitations, and scope
- Specify when the model applies and when it should not be used
- Include actual vs. predicted plots, residual diagnostics

## Key Concepts

### Prediction vs. Inference

| Aspect | Prediction | Inference |
|--------|-----------|-----------|
| Goal | Accurate forecasts on new data | Understand drivers of Y |
| Metric | Test RMSE / MSE / MAE | Coefficients, SEs, p-values, CIs |
| Interpretability | Can be a black box | Must be interpretable |
| Coefficient stability | Less critical | Critical — must be stable |

### Common Pitfalls

1. **Data Leakage**: Making preprocessing decisions (imputation, transformation, scaling) on the full dataset, then splitting. Solution: Split first, preprocess on training data only.

2. **Multicollinearity**: High correlations between predictors inflate standard errors and destroy coefficient stability. Check via correlation matrix and VIF > 5. Fix by dropping variables, regularization, or combining predictors.

3. **Ignoring Nonlinearity**: Fitting a straight line to curved data produces systematically biased predictions. Check scatter plots and residual plots. Add polynomial terms (X², X³) or transform variables (log, sqrt).

4. **Overfitting**: Too many variables relative to observations. Use AIC/BIC for variable selection or regularization (Lasso, Ridge). Always validate on held-out test set.

5. **Violating Independence Assumption**: Time series or repeated measurements have correlated errors. OLS underestimates SEs. Use time-series models or mixed-effects models instead.

### Outcome Variable Types

- **Continuous** (revenue, price, distance): Linear regression ✓
- **Count** (visits, claims): Poisson or negative binomial regression
- **Ordinal** (1–5 ratings): Ordered logistic regression
- **Binary** (yes/no): Logistic regression
- **Bounded** (0–100 percentages): Beta regression or logit-linear hybrid

## Quick Start

1. Open `index.html` in a web browser to view the interactive checklist
2. Work through each phase methodically
3. Check off completed steps using the interactive checkboxes
4. Use the progress bar to track completion
5. Reset at any time to start over

## Features

- **Interactive checklist** with phase-based organization
- **Expandable sections** for each phase
- **Progress tracking** with visual indicator
- **Dark theme** optimized for readability
- **Responsive design** for desktop and mobile
- **Reset functionality** to start over

## Technical Notes

- Built with vanilla HTML, CSS, and JavaScript
- No dependencies or external libraries
- Fully client-side (progress saved in browser localStorage)
- Works offline

## Scope Limitations

This checklist explicitly assumes:
1. **Y is continuous** — not categorical, ordinal, or count
2. **Observations are independent** — no time series, no hierarchical structure, no repeated measurements
3. **Relationships are approximately linear** — not highly nonlinear or requiring splines

If your data violates these, consult domain-specific guides for ordinal regression, count models, time series, or GAM/machine learning methods.

## Feedback & Contribution

This checklist is a living resource. Suggestions for improvements, additional phases, or clarifications are welcome.
