# Week 5 - Model Validation and Evaluation Summary

Source: `Week_5_-_Model_Validation_and_Evaluation_4859.pdf`  
Topic: CRISP-DM workflow, classification/regression evaluation, threshold tuning, and model validation

## Main idea

Week 5 explains what separates a model that "looks good" from one that is actually useful in production.

You learn to:

1. evaluate model quality with the right metrics,
2. validate generalization on unseen data,
3. align model choices with business risk and decision impact.

---

## What to know (the core concepts)

### 1) Data science workflow (CRISP-DM)

The process is iterative:

1. **Business understanding** - define objectives and constraints.
2. **Data understanding** - collect data, run EDA, assess quality.
3. **Data preparation** - clean, transform, encode, scale.
4. **Modeling** - choose algorithm, split data, train and tune.
5. **Evaluation** - compare models and check business fit.
6. **Deployment** - put model in production and monitor.

Important: You can move backward in the loop whenever new findings appear.

### 2) Classification evaluation

Start with the **confusion matrix**:

- TP (true positive)
- FP (false positive)
- FN (false negative)
- TN (true negative)

Then compute metrics:

- **Accuracy** = (TP + TN) / Total
- **Precision** = TP / (TP + FP)
- **Recall (Sensitivity, TPR)** = TP / (TP + FN)
- **Specificity (TNR)** = TN / (TN + FP)

### 3) Regression evaluation

Use residual errors:

- error_i = actual_i - predicted_i

Common metrics:

- **MAE** (Mean Absolute Error)
- **MAPE** (Mean Absolute Percentage Error)
- **MSE** (Mean Squared Error)
- **SSE** (Sum of Squared Errors)
- **R²** for goodness of fit (typically on training/fit analysis)

### 4) Threshold-based decisioning

For probabilistic classifiers, threshold choice controls trade-offs:

- lower threshold -> more positive predictions, higher recall, more FP risk
- higher threshold -> fewer positive predictions, often higher precision, more FN risk

### 5) Validation strategy

- **Training set**: learn model parameters.
- **Validation set**: tune/select models.
- **Test set**: final unbiased estimate on unseen data.

Cross-validation (especially k-fold) improves robustness during model selection.

---

## Why this matters

Accuracy alone can hide dangerous mistakes.

Example from the lecture logic:

- In medical screening, a **false negative** may be much worse than a false positive.
- Two models with the same accuracy can have very different real-world cost.

So the "best" model is not just statistical; it must satisfy:

1. business relevance,
2. operational constraints (latency, retraining cost, data collection cost),
3. regulatory and ethical requirements,
4. acceptable error cost profile.

---

## How to apply this in practice

Use this sequence when building models:

1. **Define decision context first**
   - What action follows each prediction?
   - Which error type is most costly (FP vs FN)?

2. **Prepare and split data correctly**
   - Keep test data untouched.
   - Avoid leakage from future or target-derived features.

3. **Train candidate models**
   - Compare alternatives on validation metrics, not training performance.

4. **Pick evaluation metrics aligned with risk**
   - High missed-positive cost -> optimize recall/sensitivity.
   - High false-alarm cost -> optimize precision/specificity.

5. **Tune the probability threshold**
   - Evaluate multiple threshold values.
   - Plot/inspect precision-recall and ROC behavior.
   - Select threshold based on business cost, not default 0.5.

6. **Use ROC/AUC for ranking model discrimination**
   - ROC plots TPR vs FPR across thresholds.
   - Higher AUC (closer to 1) generally indicates better separation.

7. **Test once at the end**
   - After final model + threshold selection, evaluate on test set once.

8. **Deploy with monitoring**
   - Track model drift and data drift.
   - Retrain periodically and update for compliance changes.

---

## When to use which metric

### Classification

- Use **accuracy** only when classes are balanced and error costs are similar.
- Use **recall/sensitivity** when missing positives is dangerous.
- Use **precision** when false positives are expensive.
- Use **specificity** when correctly ruling out negatives is critical.
- Use **ROC/AUC** to compare models across thresholds.
- Use **lift** when prioritizing top-ranked candidates (campaign triage, lead targeting).

### Regression

- Use **MAE** for interpretable average absolute error units.
- Use **MSE/SSE** when large errors should be penalized more strongly.
- Use **MAPE** when relative error (%) matters and targets are non-zero/stable.
- Use **R²** to describe explanatory fit, not as the only deployment metric.

---

## Overfitting and validity checklist

Before trusting a model, check:

- Does it generalize to unseen data?
- Is validation performance close to test performance?
- Are there signs of overfitting (big train-vs-test gap)?
- Does it still answer the original business question?
- Is it actionable and cost-effective to operate?
- Does it satisfy legal, ethical, and privacy constraints?

Validity types from the course:

- **Apparent validity** -> own sample (training)
- **Internal validity** -> own population (validation)
- **External validity** -> other population (test/generalization)

---

## Common mistakes to avoid

- Choosing models by accuracy only.
- Skipping validation and tuning directly on test data.
- Using the default threshold without cost analysis.
- Reporting only one metric.
- Ignoring drift after deployment.
- Treating a statistically strong model as automatically business-ready.

---

## Quick exam-ready recap (what, how, why, when)

- **What**: Evaluate models with confusion-matrix metrics (classification), residual-based metrics (regression), and proper train/validation/test design.
- **How**: Train on training data, tune with validation or cross-validation, pick threshold by cost trade-offs, and confirm once on test data.
- **Why**: Real-world decisions depend on error type and cost, not just headline accuracy.
- **When**: During model selection (validation), before release (test), and continuously after deployment (drift monitoring and retraining).
