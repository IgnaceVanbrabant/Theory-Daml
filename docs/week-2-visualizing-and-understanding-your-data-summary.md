# Week 2 - Visualizing and Understanding Your Data Summary

Source: `Week_2_-_Visualizing_and_Understanding_Your_Data_8bc9.pdf`  
Topic: Data visualization, spread, correlation, and data cleaning

## Main idea

Week 2 continues Exploratory Data Analysis (EDA). The goal is to understand data more deeply so we can describe it correctly, compare groups, find relationships, clean problems, and make better decisions.

This week focuses on:

- population vs sample,
- representativeness and sampling bias,
- measures of spread,
- skewness and kurtosis,
- correlation,
- correlation vs causation,
- one-hot encoding,
- missing values,
- handling missing data.

The important idea is that data analysis is not only about calculating numbers. It is about knowing what those numbers mean and whether they support a reliable conclusion.

---

## Population vs sample

A **population** is the full group you care about.

Examples:

- all people in Belgium,
- all EU citizens,
- all students in Belgium,
- all computer science students,
- all customers of a company.

A **sample** is a smaller part of that population.

We use samples because measuring the whole population is often impossible or too expensive. There can be limits in:

- time,
- money,
- access,
- privacy,
- available data.

### Why this matters

Most data analysis uses samples, but we usually want to say something about the bigger population. That only works if the sample is good enough.

For example, if you want to know how much young people like coding, asking only computer science students will probably give a biased answer. They are more likely to like computers than the average young person.

---

## Representativeness and sampling bias

A sample is **representative** when it reasonably reflects the population you want to study.

A sample is **biased** when some groups are overrepresented or underrepresented.

Example question:

> How much do young people like coding and working with computers?

Possible samples:

- people present in a computer science lecture,
- the first 200 young people found in one shopping street,
- students from different high schools, with a few people asked at each school.

The third option is probably better because it includes more different groups. The first option is likely biased because computer science students already have an interest in computers.

### Why this matters

If the sample is biased, the conclusion can be wrong even if the calculations are correct.

Good data analysis asks:

- Who is included in the sample?
- Who is missing?
- Does the sample match the population?
- Could the way we collected data influence the result?

---

## Measures of spread

Spread, also called **variability**, describes how far apart the values in a dataset are.

Two datasets can have the same average but very different spread.

Example:

```text
Dataset A: 48, 49, 50, 51, 52
Dataset B: 10, 30, 50, 70, 90
```

Both can have the same center, but Dataset B is much more spread out.

### Why spread matters

Spread helps understand:

- consistency,
- risk,
- reliability,
- volatility,
- uncertainty,
- how much values differ from the typical value.

Examples:

- In finance, high spread can mean high risk.
- In manufacturing, high spread can mean inconsistent quality.
- In customer ratings, high spread can mean mixed opinions.
- In travel costs, high spread can mean packages vary strongly in price.

---

## Mean Absolute Deviation, variance, and standard deviation

These are common ways to measure spread.

### Mean Absolute Deviation (MAD)

MAD is the average absolute distance between each value and the mean.

Formula idea:

```text
MAD = average of |value - mean|
```

MAD is easy to understand because it tells you the average distance from the mean.

### Variance

Variance is the average squared distance from the mean.

Formula idea:

```text
variance = average of (value - mean)^2
```

Variance gives more weight to large differences because the differences are squared.

### Standard deviation

Standard deviation is the square root of the variance.

Formula idea:

```text
standard deviation = square root of variance
```

Standard deviation is commonly used because it is in the original units of the data.

For example:

- if cost is measured in euros, standard deviation is also in euros,
- if stay length is measured in days, standard deviation is also in days.

---

## Why absolute values and squares are used

If we simply add the differences from the mean, positive and negative differences cancel out.

Example:

```text
-5 + 5 = 0
```

That would make the spread look smaller than it really is.

To avoid this:

- MAD uses absolute values,
- variance uses squared values.

### Difference between MAD and variance

MAD treats distances more directly.

Variance punishes large deviations more strongly because it squares the distance. This makes variance and standard deviation more sensitive to outliers.

---

## Comparing spread measures

| Measure | What it does | Strength | Weakness |
| --- | --- | --- | --- |
| MAD | Average absolute distance from mean | Easy to understand | Less common in practice |
| Variance | Average squared distance from mean | Strongly shows large deviations | Units are squared, so harder to interpret |
| Standard deviation | Square root of variance | Common and uses original units | Sensitive to outliers |

Use spread together with the mean or median. A center value alone does not show how consistent the data is.

---

## Skewness

**Skewness** describes whether a distribution is symmetrical or has a longer tail on one side.

### Positive skew

Positive skew is also called right skew.

Most values are lower, but a few high values stretch the right side.

Example:

- most trips are cheap,
- a few luxury trips are very expensive.

In positive skew, the mean is often higher than the median because the high values pull the mean upward.

### Negative skew

Negative skew is also called left skew.

Most values are higher, but a few low values stretch the left side.

Example:

- most ratings are high,
- a few very low ratings pull the distribution left.

### Why skewness matters

Skewness tells you whether the mean is a good summary. If data is strongly skewed, the median may better describe the typical value.

---

## Kurtosis

**Kurtosis** describes the tail behavior and peak shape of a distribution. It focuses on how likely extreme values are.

### High kurtosis

High kurtosis means:

- sharper peak,
- heavier tails,
- more extreme values,
- more influence from outliers.

This is also called **leptokurtic**.

### Low kurtosis

Low kurtosis means:

- flatter distribution,
- thinner tails,
- fewer extreme values.

This is also called **platykurtic**.

### Why kurtosis matters

Kurtosis helps show whether extreme values are common enough to worry about. This matters for risk, outlier detection, and understanding how stable the data is.

---

## Correlation

**Correlation** measures the relationship between two variables.

It asks:

> When one variable changes, what tends to happen to the other variable?

The correlation coefficient is usually written as **r**.

| r value | Meaning |
| --- | --- |
| `r = 1` | Perfect positive linear relationship |
| `r = -1` | Perfect negative linear relationship |
| `r = 0` | No linear relationship |

### Positive correlation

When one variable increases, the other also tends to increase.

Example:

- longer stay length may be related to higher trip cost.

### Negative correlation

When one variable increases, the other tends to decrease.

Example:

- higher discount may be related to lower margin.

### No correlation

The variables do not move together in a clear linear way.

Important: correlation measures **linear** relationships. If a relationship is curved or more complex, correlation may not show it clearly.

---

## Correlation matrix

A **correlation matrix** shows correlations between many numeric variables at once.

It is useful when a dataset has many columns and you want to quickly see which variables move together.

Example uses:

- cost vs margin,
- stay length vs cost,
- guests vs cost,
- rating vs margin,
- discount vs margin.

Correlation matrices can help find patterns, but they should not be treated as proof of cause.

---

## Correlation is not causation

This is one of the most important ideas in the lecture.

If two variables are correlated, it does not automatically mean that one causes the other.

Example from the PDF:

- ice cream sales and drownings can both increase in summer.

That does not mean ice cream causes drowning. A third factor, hot weather, may influence both.

### Why this matters

Confusing correlation with causation can lead to bad decisions.

Example:

- homes with more books may be correlated with better academic results,
- but simply mailing books to homes may not fix the real causes,
- because the real explanation could involve parents, income, education, environment, or other factors.

Before claiming cause, ask:

- Is there a logical explanation?
- Could another variable explain both?
- Was there an experiment?
- Is there enough evidence?

---

## Spurious correlations

A **spurious correlation** is a relationship that appears in the data but is not meaningful.

It can happen by coincidence, especially in large datasets with many variables.

The more variables you compare, the more likely you are to find random patterns.

### How to avoid being fooled

Always ask:

- Does this relationship make sense?
- Is there domain knowledge supporting it?
- Could it be coincidence?
- Could a hidden third variable explain it?
- Should we test it further?

Correlation is useful for finding possible relationships, but it is not enough by itself.

---

## One-hot encoding

Many statistics and machine-learning methods need numeric data. But many useful columns are categorical.

Example categorical values:

- red, green, blue,
- standard, silver, gold,
- relaxation, cultural, adventure,
- Belgium, France, Germany.

**One-hot encoding** converts categories into numeric binary columns.

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

### Why this is useful

After encoding, categorical variables can be used in numeric analysis and machine-learning models.

For example, we could analyze how destination or package type relates to cost or margin.

---

## Missing values

Missing values are values that should be in the dataset but are absent.

Examples:

- a customer has no age listed,
- a trip has no cost listed,
- a customer has no country listed,
- a student has no SAT score listed.

Missing values matter because they can bias results or reduce the amount of usable data.

---

## Types of missingness

### Missing Completely at Random (MCAR)

The missing value is unrelated to anything in the data.

Example:

- a participant accidentally skips a survey question,
- a random technical issue causes some transactions to be lost.

MCAR is usually the least dangerous type because the missingness is random.

### Missing at Random (MAR)

The missingness is related to another observed variable, but not directly to the missing value itself.

Example:

- younger people are less likely to answer a certain survey question.

The missingness depends on age, which is observed.

### Missing Not at Random (MNAR)

The missingness is related to the missing value itself.

Example:

- people with high income do not want to report their income,
- firms in financial trouble do not want to disclose earnings.

MNAR is dangerous because the missing data is connected to the thing you are trying to measure.

---

## Handling missing values

There is no single best method. The right choice depends on why the values are missing and what analysis you want to do.

### 1. Remove missing data

You can delete rows with missing values.

Advantage:

- simple.

Disadvantage:

- you may lose important data,
- the remaining data may become biased.

### 2. Use available data only

You can skip missing values only when that variable is needed.

Advantage:

- keeps more rows.

Disadvantage:

- different analyses may use different subsets of data, which can make results inconsistent.

### 3. Impute missing values

Imputation means filling in missing values.

Possible replacements:

- 0,
- mean,
- median,
- mode,
- predicted value.

Be careful: replacing missing values can introduce bias. Replacing with 0 is often a bad idea unless 0 has a real meaning.

### 4. Mark missing values

Sometimes missingness itself is useful information.

You can add a column showing whether a value was missing.

Example:

```text
Income_missing = 1
```

This can help detect patterns in missingness.

---

## Good missing-value practice

Before handling missing values:

1. Check how many values are missing.
2. Check which columns have missing values.
3. Think about why the values are missing.
4. Decide whether the missingness is MCAR, MAR, or MNAR.
5. Choose a method that fits the analysis.
6. Document what you did.

Documenting matters because missing-value handling changes the dataset and affects interpretation.

---

## Simple Week 2 workflow

A good workflow for this lecture is:

1. **Define the population and sample**  
   Know who or what you want to study and what data you actually have.

2. **Check representativeness**  
   Ask whether the sample could be biased.

3. **Summarize the center and spread**  
   Use mean, median, MAD, variance, and standard deviation where useful.

4. **Check shape**  
   Look for skewness, heavy tails, and extreme values.

5. **Look for relationships**  
   Use correlation for numeric variables.

6. **Avoid false conclusions**  
   Remember that correlation is not causation.

7. **Prepare categorical data**  
   Use one-hot encoding when categorical values need to become numeric.

8. **Handle missing values carefully**  
   Understand why values are missing before removing or imputing them.

9. **Document decisions**  
   Write down cleaning choices so the analysis is reproducible.

---

## Key takeaways

- A population is the full group of interest; a sample is the part you actually observe.
- A biased sample can produce wrong conclusions even with correct calculations.
- Spread shows how consistent or variable the data is.
- MAD, variance, and standard deviation all measure spread in different ways.
- Standard deviation is common because it uses the original data units.
- Skewness shows whether a distribution has a longer tail on one side.
- Kurtosis shows how much extreme values matter.
- Correlation measures linear relationships between variables.
- Correlation does not prove causation.
- Spurious correlations can appear by chance, especially in large datasets.
- One-hot encoding turns categorical data into numeric binary columns.
- Missing values can be MCAR, MAR, or MNAR.
- Missing data should be handled based on why it is missing.
- Always document how data was cleaned.
