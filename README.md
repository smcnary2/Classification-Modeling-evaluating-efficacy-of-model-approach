# Classification-Modeling-evaluating-efficacy-of-model-approach

# Logistic vs Sinusoidal Probabilistic Modeling in R

## Overview
This project compares two approaches for modeling binary outcomes generated from an underlying oscillating (sinusoidal) probability function:

1. **Logistic Regression** – a standard generalized linear model for binary outcomes.
2. **Nonlinear Sinusoidal Model** – a nonlinear least squares model designed to capture periodic structure in the data.

The goal is to evaluate how well each model predicts probabilities under uncertainty using:
- Cross-entropy (log loss)
- Area Under the ROC Curve (AUC)

---

## Motivation
Binary classification models often assume monotonic relationships between predictors and outcomes. However, real-world systems can exhibit **periodic or cyclic behavior**. This script demonstrates how a standard logistic regression can fail to capture such structure and how a nonlinear sinusoidal model may better represent the data-generating process.

---

## Data Generation
- `x` is generated uniformly on `[0, 10]`
- The true probability of success is:
  
  \[
  p(x) = \frac{\sin(x) + 1}{2}
  \]

- Binary outcomes are sampled using a Bernoulli process:
  
  ```r
  y <- rbinom(200, 1, true_prob)

## Results & Visualization

The figure below compares observed binary outcomes with predicted probabilities from both models.

- Gray points represent observed binary outcomes.
- The green dashed line shows logistic regression predictions.
- The blue solid line shows sinusoidal model predictions.

### Interpretation
The logistic regression model produces a smooth, monotonic probability curve and is unable to capture the periodic structure present in the data. As a result, it systematically underfits regions where the true probability oscillates.

In contrast, the sinusoidal model closely follows the underlying oscillatory pattern, resulting in better alignment with observed outcomes across the domain.

This visual difference is consistent with quantitative results:
- Lower cross-entropy for the sinusoidal model
- Higher AUC, indicating improved class separation

Together, the visualization and metrics demonstrate the importance of aligning model assumptions with the true data-generating process.

