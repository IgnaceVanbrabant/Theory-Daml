# Week 4 - Regression and Distributions Summary

Source: `Week_4_-_Regression_and_Distributions_6df3.pdf`  
Topic: Linear regression, logistic regression, distributions, significance testing, and confidence intervals

## Main idea

Week 4 combines two core skills:

1. **Building prediction models** (linear and logistic regression).
2. **Interpreting uncertainty** (distributions, p-values, and confidence intervals).

These topics work together: machine learning gives predictions, and statistics helps you judge whether those predictions and patterns are reliable.

---

## Why we do this

We study this because real-world decisions need more than raw numbers.

- Businesses need to predict outcomes (cost, demand, churn, fraud risk).
- Teams need to understand how uncertain those predictions are.
- Analysts need to avoid false conclusions from random noise.

In short:

> Regression helps us predict.  
> Distributions and inference help us trust (or question) those predictions.

---

## What it does

Week 4 gives you a practical toolkit to:

- predict continuous values with **linear regression**,
- predict class probabilities with **logistic regression**,
- choose and interpret probability **distributions**,
- evaluate evidence with **hypothesis tests** and **p-values**,
- communicate uncertainty using **confidence intervals**,
- distinguish **statistical significance** from **practical significance**.

---

## Supervised learning refresher

Supervised learning learns from labeled examples.

- **Classification**: predict a category (yes/no, class A/B/C).
- **Regression**: predict a numeric value.

Week 4 focuses on regression models plus statistical foundations that support model interpretation.

---

## Linear regression

Linear regression predicts a numeric target.

### Simple linear regression

One predictor:

```text
y = beta0 + beta1 * X + error
```

### Multiple linear regression

Multiple predictors:

```text
y = beta0 + beta1*x1 + beta2*x2 + ... + betap*xp + error
```

### Interpretation

- `beta0`: intercept (baseline prediction).
- `beta1 ... betap`: change in `y` when a predictor changes (holding others constant).
- `error`: noise and unmodeled factors.

Use linear regression when the target is continuous (e.g., loan amount, sales, price).

---

## Logistic regression

Logistic regression is used for classification, usually binary outcomes.

It starts with a linear score and applies the **sigmoid** function:

```text
sigmoid(z) = 1 / (1 + e^(-z))
```

This maps outputs to `[0, 1]`, so they can be interpreted as probabilities.

### Why logistic instead of linear for class labels

Linear regression can output values below 0 or above 1, which are invalid probabilities.
Logistic regression keeps outputs in range and is naturally probabilistic.

### Threshold

A threshold converts probability to class label:

- if `p >= threshold` -> class 1
- else -> class 0

Changing threshold trades off false positives and false negatives (precision vs recall).

---

## Regularization

Regularization penalizes complexity to reduce overfitting.

- **Lasso (L1)**: can shrink some coefficients to zero (feature selection effect).
- **Ridge (L2)**: shrinks coefficients toward smaller values.

Practical takeaway: simpler models often generalize better.

---

## Statistical distributions

A distribution describes how values are spread.

### Continuous distributions

- **Normal**: bell-shaped; common in natural and measurement processes.
- **Student t**: similar to normal but heavier tails; useful for smaller samples or unknown population standard deviation.
- **Exponential**: models waiting time or time between events.

### Discrete distributions

- **Uniform**: equal probability outcomes (e.g., fair die).
- **Poisson**: count of events in a fixed interval.
- **Bernoulli**: one binary trial (0/1).
- **Binomial**: number of successes across multiple Bernoulli trials.

### 68-95-99.7 rule (normal distribution)

- ~68% within 1 standard deviation of mean.
- ~95% within 2 standard deviations.
- ~99.7% within 3 standard deviations.

---

## Statistical significance

### Null hypothesis (H0)

Assumes no effect or no difference.

### P-value

Probability of seeing results as extreme as observed if `H0` is true.

- `p < alpha` -> reject `H0` (statistically significant evidence).
- `p > alpha` -> fail to reject `H0`.

Common alpha values: 0.10, 0.05, 0.01.

---

## Confidence intervals

A confidence interval gives a plausible range for the true population parameter.

- Built from point estimate +/- margin of error.
- Higher confidence level -> wider interval.

Interpretation example:

A 95% CI means that over many repeated samples, about 95% of similarly built intervals would contain the true value.

---

## Statistical vs practical significance

- **Statistical significance**: effect is unlikely due to random chance.
- **Practical significance**: effect is large enough to matter in real life.

A tiny effect can be statistically significant in very large samples but still not useful.

---

## How to use this correctly

Use this checklist when applying Week 4 concepts:

1. **Define the target clearly**
   - Numeric target -> regression.
   - Binary/categorical target -> classification (often logistic for binary).

2. **Match model to problem**
   - Linear regression for continuous outcomes.
   - Logistic regression for probabilities of class membership.

3. **Validate assumptions**
   - Check data quality and feature relevance.
   - For inference, choose distributions and tests that fit your sample and context.

4. **Tune decision threshold by risk**
   - In high-risk domains (e.g., medical screening), reduce dangerous false negatives even if false positives increase.

5. **Control overfitting**
   - Use regularization (L1/L2), especially with many predictors.

6. **Report uncertainty, not just point predictions**
   - Include confidence intervals and significance context.

7. **Avoid common mistakes**
   - Do not treat p-value as effect size.
   - Do not equate statistical significance with business value.
   - Be careful with multiple comparisons and p-hacking risks.

---

## Quick workflow

1. Define question and target.
2. Prepare predictors and clean data.
3. Choose model (linear/logistic).
4. Train and evaluate.
5. Apply regularization if needed.
6. Interpret outputs with p-values/CIs.
7. Check practical impact before decisions.

---

## Key takeaways

- Linear regression predicts numbers; logistic regression predicts class probabilities.
- Distributions help model uncertainty and choose proper statistical tools.
- P-values test evidence against a null hypothesis, but do not measure practical value.
- Confidence intervals communicate estimation uncertainty clearly.
- Correct use means combining model output, statistical evidence, and real-world impact.
