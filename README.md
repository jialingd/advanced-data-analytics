Predictive Modeling of Violent Recidivism Using the COMPAS Dataset

This project focuses on predictive modeling of violent recidivism using the COMPAS dataset.
The code evaluates and compares several statistical learning models — logistic regression (GLM), generalized additive models (GAM), and decision trees — to assess their performance, interpretability, and fairness relative to the proprietary COMPAS risk score used in U.S. pretrial decisions.

🧠 Objectives

Build interpretable statistical models to predict violent re-arrest within two years.

Compare predictive accuracy, calibration, and bias of GAM, GLM, and decision tree models.

Benchmark these models against the commercial COMPAS algorithm.

Evaluate performance trade-offs (accuracy, FPR/FNR, calibration) and discuss ethical implications of algorithmic decision-making in the criminal justice system.

📊 Data

The dataset contains pretrial defendant records including:

Demographics: age, sex, race

Criminal history: prior counts, charges

Outcome: re-arrest for violent crime within 2 years

COMPAS score: 1–10 ordinal risk rating

Data preprocessing steps:

Randomly split data into training and testing sets.

Ensure unbiased model validation by using the test set for final performance reporting.

Handle class imbalance and missing values as noted in code comments.

 
 Analysis Steps

1.  Baseline Evaluation

Estimate base recidivism rate (~18.4%) on test set.

Justify random train/test splitting for unbiased performance estimation.

2.  Logistic Regression (GLM)

Model: recidivism ~ age + priors_count

Interpret log-odds coefficients:

Older individuals less likely to recidivate (β_age < 0)

Prior convictions increase risk (β_priors > 0)

Compute predicted probabilities with 95% confidence intervals for four example profiles (Archie, Betty, Chuck, Veronica).

3. Threshold Analysis

Examine accuracy, false-positive rate (FPR), and false-negative rate (FNR) as functions of the classification threshold.

Identify optimal threshold ≈ 0.39, with baseline accuracy ≈ 0.816.

4.  Generalized Additive Model (GAM)

Model nonlinear smooths of age and priors_count.

Visualize smooth functions s(age) and s(priors_count) to capture diminishing marginal effects.

Compare GAM vs. logistic regression accuracy curves — GAM slightly better at low thresholds, comparable at moderate ones.

5.  Decision Tree Model

Construct decision tree using recursive partitioning.

Visualize splits on age and priors_count.

Discuss over-simplified output (predicts mostly “no recidivism”) and its limited predictive power.

6.  Model Comparison

Generate accuracy vs. threshold plots for all models (GLM, GAM, Decision Tree).

FNR vs. FPR curves show GAM and GLM outperform Decision Tree in stability and calibration.

Calibration plots demonstrate GAM’s superior alignment with observed recidivism frequencies.

7.  COMPAS Benchmark

Evaluate COMPAS threshold-based accuracy and FNR/FPR.

Show that COMPAS performs near baseline accuracy, below GAM/GLM models.

Illustrate bias via FNR–FPR plots by race and sex, revealing demographic disparities in algorithmic predictions.

8. Residual Diagnostics

Plot residuals and squared residuals vs. predicted probabilities for all models.

Verify that residual patterns support homoscedasticity and model calibration assumptions.

9.  Model Recommendation

Recommend GAM for Riverdale County’s pretrial screening system:

Well-calibrated and interpretable

Captures nonlinear effects while avoiding overfitting

Logistic regression serves as the next-best alternative if simplicity is prioritized.
