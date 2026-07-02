# Week 2 - Visualizing and Understanding Your Data Summary

Source: `Week_2_-_Visualizing_and_Understanding_Your_Data_8bc9.pdf`  
Topic: Data visualization, spread, correlation, and data cleaning

## Main idea

Week 2 continues Exploratory Data Analysis (EDA). The goal is to understand data well enough to describe it, compare it, find patterns, clean problems, and make better decisions.

The useful topics are:

- population vs sample,
- representativeness and sampling bias,
- spread and variability,
- MAD, variance, and standard deviation,
- skewness and kurtosis,
- correlation,
- correlation vs causation,
- spurious correlations,
- one-hot encoding,
- missing values and how to handle them.

---

## Population vs sample

A **population** is the full group you care about.

Examples:

- all Belgian people,
- all EU citizens,
- all students in Belgium,
- all customers of a company.

A **sample** is a smaller part of that population.

We usually use samples because studying the full population takes too much time, money, or access.

Important: conclusions from a sample are only useful if the sample reasonably represents the population.

---

## Representativeness and sampling bias

A sample is **representative** when it looks enough like the population you want to study.

A sample is **biased** when some groups are included too much or too little.

Example:

If you want to know how much young people like coding, asking only computer science students is biased because they are already more interested in computers.

Better sampling means including different groups from the population.

When checking a sample, ask:

- Who is included?
- Who is missing?
- Was the data collected in a fair way?
- Could the sample change the conclusion?

---

## Measures of spread

**Spread** means how far apart the values in a dataset are.

Two datasets can have the same average but different spread:

```text
Dataset A: 48, 49, 50, 51, 52
Dataset B: 10, 30, 50, 70, 90
```

Both are centered around 50, but Dataset B is much more spread out.

Spread is useful because it shows:

- consistency,
- risk,
- reliability,
- volatility,
- how different values are from the typical value.

Examples:

- High spread in prices means prices vary a lot.
- High spread in ratings means customers disagree.
- High spread in production quality means the process is unreliable.

---

## MAD, variance, and standard deviation

These three statistics measure spread.

### Mean Absolute Deviation (MAD)

MAD is the average absolute distance from the mean.

```text
MAD = average of |value - mean|
```

It is easy to understand because it tells you the average distance from the mean.

### Variance

Variance is the average squared distance from the mean.

```text
variance = average of (value - mean)^2
```

It gives more weight to large differences because the distances are squared.

### Standard deviation

Standard deviation is the square root of variance.

```text
standard deviation = square root of variance
```

It is commonly used because it is in the original units of the data.

Example:

- if cost is in euros, standard deviation is also in euros,
- if stay length is in days, standard deviation is also in days.

### Why not use normal differences?

If we add normal differences from the mean, positive and negative values cancel out.

```text
-5 + 5 = 0
```

That would hide the real spread. Absolute values and squares prevent this.

---

## Comparing spread measures

| Measure | Meaning | Main point |
| --- | --- | --- |
| MAD | Average absolute distance from mean | Easy to interpret |
| Variance | Average squared distance from mean | Strongly affected by large deviations |
| Standard deviation | Square root of variance | Common and uses original units |

Standard deviation is very useful, but it is sensitive to outliers.

---

## Skewness

**Skewness** describes whether data is symmetrical or has a longer tail on one side.

### Positive skew

Positive skew, or right skew, means most values are lower, but a few high values stretch the right side.

Example:

- most trips are cheap,
- a few luxury trips are very expensive.

The mean is often higher than the median because high values pull it upward.

### Negative skew

Negative skew, or left skew, means most values are higher, but a few low values stretch the left side.

Example:

- most ratings are high,
- a few very low ratings pull the distribution left.

Skewness matters because strongly skewed data may be better summarized with the median than the mean.

---

## Kurtosis

**Kurtosis** describes how extreme the tails of a distribution are.

High kurtosis means:

- sharper peak,
- heavier tails,
- more extreme values,
- more outlier influence.

Low kurtosis means:

- flatter distribution,
- thinner tails,
- fewer extreme values.

Kurtosis is useful when you care about risk and extreme cases.

---

## Correlation

**Correlation** measures the relationship between two variables.

It asks:

> When one variable increases, what happens to the other variable?

The correlation coefficient is written as **r**.

| r value | Meaning |
| --- | --- |
| `r = 1` | Perfect positive linear relationship |
| `r = -1` | Perfect negative linear relationship |
| `r = 0` | No linear relationship |

Examples:

- Positive correlation: longer trips may cost more.
- Negative correlation: higher discounts may reduce margin.
- No correlation: two variables do not move together clearly.

Important: correlation measures **linear** relationships. A curved relationship may not be captured well.

---

## Correlation matrix

A **correlation matrix** shows correlations between many numeric variables at once.

It helps quickly find possible relationships, such as:

- cost vs margin,
- stay length vs cost,
- guests vs cost,
- discount vs margin,
- rating vs package features.

A correlation matrix is useful for exploration, but it does not prove cause.

---

## Correlation is not causation

Correlation does not mean one variable causes the other.

Example:

Ice cream sales and drownings can both increase in summer. That does not mean ice cream causes drowning. Hot weather is probably influencing both.

Bad decisions happen when correlation is treated as proof.

Before claiming causation, ask:

- Is there a logical reason?
- Could a third variable explain it?
- Was there an experiment?
- Is there enough evidence?

---

## Spurious correlations

A **spurious correlation** is a relationship that appears in the data but is not meaningful.

This happens more often in large datasets because many variables are compared. The more relationships you search for, the more random patterns you may find.

To avoid being fooled, ask:

- Does the relationship make sense?
- Is there domain knowledge supporting it?
- Could it be coincidence?
- Could another variable explain it?
- Should it be tested further?

---

## One-hot encoding

Many calculations and machine-learning models need numeric input. Categorical data often needs to be converted first.

**One-hot encoding** turns categories into binary columns.

Example:

Original column:

| Color |
| --- |
| Green |
| Blue |
| Red |

After one-hot encoding:

| Color_Green | Color_Blue | Color_Red |
| --- | --- | --- |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 1 |

This makes it possible to use categories like package type, destination, or membership level in numeric analysis.

---

## Missing values

Missing values are values that are absent from the dataset.

Examples:

- missing customer age,
- missing trip cost,
- missing country,
- missing test score.

Missing values matter because they can bias results or reduce usable data.

---

## Types of missingness

### MCAR: Missing Completely at Random

The missingness is unrelated to the data.

Example:

- a random technical problem loses some transactions.

### MAR: Missing at Random

The missingness is related to another observed variable, but not directly to the missing value itself.

Example:

- younger people are less likely to answer a certain question.

### MNAR: Missing Not at Random

The missingness is related to the missing value itself.

Examples:

- people with high income do not report income,
- companies in financial trouble do not report earnings.

MNAR is the most dangerous because the missing data is connected to the thing you want to measure.

---

## Handling missing values

There is no single best solution. First understand why the data is missing.

Possible methods:

### Remove rows

Simple, but you may lose important data or create bias.

### Use available data only

Keeps more rows, but different analyses may use different subsets.

### Impute values

Fill in missing values with something like:

- mean,
- median,
- mode,
- predicted value.

Be careful: imputation can introduce bias. Replacing with 0 is often bad unless 0 has a real meaning.

### Mark missingness

Add a column showing whether a value was missing.

Example:

```text
Income_missing = 1
```

This is useful when missingness itself contains information.

---

## Simple Week 2 workflow

1. **Define the population**  
   Know who or what you want to study.

2. **Check the sample**  
   Ask whether it represents the population.

3. **Measure center and spread**  
   Use mean, median, MAD, variance, and standard deviation.

4. **Check shape**  
   Look for skewness, kurtosis, and outliers.

5. **Look for relationships**  
   Use correlation and correlation matrices.

6. **Avoid false conclusions**  
   Remember that correlation is not causation.

7. **Convert categories if needed**  
   Use one-hot encoding for categorical variables.

8. **Handle missing values carefully**  
   Decide whether values are MCAR, MAR, or MNAR.

9. **Document your choices**  
   Cleaning decisions affect the final interpretation.

---

## Key takeaways

- A population is the full group; a sample is the part you observe.
- Samples must be representative to support good conclusions.
- Spread shows how variable or consistent data is.
- MAD, variance, and standard deviation measure spread differently.
- Standard deviation is common because it uses the original units.
- Skewness shows whether data has a long tail on one side.
- Kurtosis shows how much extreme values matter.
- Correlation measures linear relationships.
- Correlation does not prove causation.
- Spurious correlations can happen by chance.
- One-hot encoding turns categories into numeric columns.
- Missing values can be MCAR, MAR, or MNAR.
- Missing data should be handled carefully and documented.
