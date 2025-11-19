# Predictive Modeling of Violent Recidivism Using the COMPAS Dataset

## Overview
This project analyzes the COMPAS dataset to build interpretable statistical models for predicting violent recidivism. The research evaluates and compares multiple statistical learning approaches — logistic regression (GLM), generalized additive models (GAM), and decision trees — assessing their performance, interpretability, and fairness relative to the proprietary COMPAS risk score used in U.S. pretrial decisions.

## Objectives
- Build interpretable statistical models to predict violent re-arrest within two years
- Compare predictive accuracy, calibration, and bias across GAM, GLM, and decision tree models
- Benchmark against the commercial COMPAS algorithm
- Evaluate performance trade-offs (accuracy, FPR/FNR, calibration) and discuss ethical implications of algorithmic decision-making in criminal justice

## 📊 Dataset
The dataset contains pretrial defendant records including:
- **Demographics**: age, sex, race
- **Criminal history**: prior counts, charges  
- **Outcome**: re-arrest for violent crime within 2 years
- **COMPAS score**: 1–10 ordinal risk rating

### Data Preprocessing
- Randomly split data into training and testing sets
- Ensure unbiased model validation using test set for final performance reporting
- Handle class imbalance and missing values as documented in code

##  Analysis Approach

### 1. Baseline Evaluation
- Estimate base recidivism rate (~18.4%) on test set
- Validate random train/test splitting for unbiased performance estimation

### 2. Logistic Regression (GLM)
- Model: `recidivism ~ age + priors_count`
- Key findings:
  - Older individuals less likely to recidivate (β_age < 0)
  - Prior convictions increase risk (β_priors > 0)
- Compute predicted probabilities with 95% confidence intervals for example defendant profiles

### 3. Threshold Analysis
- Examine accuracy, FPR, and FNR across classification thresholds
- Identify optimal threshold ≈ 0.39 with baseline accuracy ≈ 0.816

### 4. Generalized Additive Model (GAM)
- Model nonlinear smooths of age and priors_count
- Visualize smooth functions capturing diminishing marginal effects
- GAM shows slightly better performance at low thresholds compared to logistic regression

### 5. Decision Tree Model
- Construct decision tree using recursive partitioning
- Visualize splits on age and priors_count
- Model shows limited predictive power, predicting mostly "no recidivism"

### 6. Model Comparison
- Accuracy vs. threshold plots show GAM and GLM outperform Decision Tree
- FNR vs. FPR curves demonstrate superior stability and calibration for GAM/GLM
- Calibration plots confirm GAM's better alignment with observed recidivism frequencies

### 7. COMPAS Benchmark
- COMPAS performs near baseline accuracy, below GAM/GLM models
- Bias analysis via FNR–FPR plots reveals demographic disparities by race and sex

### 8. Residual Diagnostics
- Plot residuals and squared residuals vs. predicted probabilities
- Verify homoscedasticity and model calibration assumptions

## Model Recommendation
**GAM** is recommended for Riverdale County's pretrial screening system due to:
- Superior calibration and interpretability
- Ability to capture nonlinear effects without overfitting
- Balanced performance across metrics

**Logistic regression** serves as a viable alternative when model simplicity is prioritized.

## ⚖️ Ethical Considerations
The analysis highlights important ethical implications regarding algorithmic fairness, demographic biases in risk assessment tools, and the responsibility in deploying predictive models in criminal justice contexts.
