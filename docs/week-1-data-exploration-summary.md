# Week 1 - Data Exploration Summary

Source: `Week_1_-_Data_Exploration_ce24.pdf`  
Topic: Exploratory Data Analysis (EDA)

## Main idea

Exploratory Data Analysis, or **EDA**, is the step where you first try to understand a dataset before using it for decisions, statistics, or machine learning.

The goal is to answer questions like:

- What data do we have?
- What does each column mean?
- Which columns are numbers, categories, or ordered values?
- Are there mistakes, missing values, or strange values?
- What is typical in the data?
- Are there patterns that can help make business decisions?

EDA matters because a model or calculation is only useful if the data is understood correctly first.

---

## Case study: travel agency data

The lecture uses a travel agency dataset. The data describes sales, customers, travel packages, prices, profit, discounts, and ratings.

Important columns include:

| Column | What it means | Why it is useful |
| --- | --- | --- |
| `SalesID` | Unique sale ID | Identifies each sale. |
| `Age` | Customer age | Helps understand customer groups. |
| `Country` | Customer country | Shows where customers come from. |
| `Membership` | Standard, silver, or gold | Shows customer loyalty level. |
| `Previous_Purchases` | Number of earlier purchases | Helps identify returning customers. |
| `Package type` | Relaxation, cultural, adventure | Shows what kind of trip was sold. |
| `Destination` | Travel destination | Helps find popular destinations. |
| `Cost` | Cost or price-related value | Used for pricing and revenue analysis. |
| `Margin` | Profit margin | Shows profitability. |
| `Guests` | Number of travelers | Shows booking size. |
| `Stay_length` | Trip length | Helps compare short and long trips. |
| `Travel_month` | Month of travel | Useful for seasonal trends. |
| `Earlybird discount` | Whether discount was used | Helps evaluate promotions. |
| `Rating` | Customer score | Measures customer satisfaction. |

Useful questions for this dataset:

- Which package type sells the most?
- Which package type has the highest cost?
- Which package type has the highest margin?
- Which destinations are popular?
- Do discounts affect sales or margins?
- Can historical data help set better prices?

---

## Data types

Understanding data types is one of the most important parts of EDA. The type of data decides which calculations and charts make sense.

### 1. Continuous numeric data

Continuous numeric data can take many possible values, including decimals.

Examples:

- cost,
- margin,
- price,
- time,
- distance.

Useful statistics:

- mean,
- median,
- minimum,
- maximum,
- range,
- quartiles.

Important: some values must follow real-world rules. For example, cost should normally be positive.

### 2. Discrete numeric data

Discrete numeric data uses countable values.

Examples:

- rating from 1 to 5,
- number of guests,
- number of previous purchases,
- number of travel days.

You can count these values, compare them, and sometimes average them. But an average may create a value that does not actually exist, such as an average rating of 4.3.

### 3. Nominal categorical data

Nominal categorical data contains labels without a natural order.

Examples:

- country,
- destination,
- package type.

You can count categories and find the most common one, but you should not calculate a mean for them.

### 4. Binary data

Binary data has two possible values.

Examples:

- paid/unpaid,
- discount/no discount,
- yes/no,
- true/false,
- 1/0.

Binary data is useful for filtering, counting, and comparing groups.

### 5. Ordinal categorical data

Ordinal categorical data has categories with a meaningful order.

Example:

```text
Standard < Silver < Gold
```

The order matters, but the distance between levels is not always equal. Gold is higher than silver, but that does not automatically mean it is exactly twice as valuable.

---

## Important summary statistics

Summary statistics reduce a lot of data into a few useful numbers.

### Mean

The **mean** is the average.

```text
mean = sum of all values / number of values
```

Use it for numeric data when you want a quick overall value.

Examples:

- average cost,
- average margin,
- average rating,
- average stay length.

Be careful: the mean is strongly affected by extreme values.

Example idea from the lecture: the average number of legs per person can be less than 2, even though most people have 2 legs. This shows that the mean is not always the same as what is typical or most common.

### Median

The **median** is the middle value after sorting the data.

Use it when data is skewed or has outliers.

Example:

```text
[10, 10, 10, 10, 10, 10, 50, 300]
```

The value `300` pulls the mean upward, but the median still better represents the typical value.

### Mode

The **mode** is the most frequent value.

Use it for categorical data or repeated values.

Examples:

- most common package type,
- most common destination,
- most common membership level,
- most common rating.

---

## Outliers

An **outlier** is a value that is very different from the rest of the data.

Possible causes:

- typing mistakes,
- wrong units,
- measurement errors,
- rare but real cases,
- unusual customers or products.

Outliers matter because they can change the mean, stretch graphs, and lead to wrong conclusions.

Do not delete outliers automatically. First check whether they are errors or real important cases.

---

## Quartiles and box plots

Quartiles help describe the spread of numeric data.

- **Q1**: first quartile, around the 25% point.
- **Q2**: median, around the 50% point.
- **Q3**: third quartile, around the 75% point.

The **interquartile range** is:

```text
IQR = Q3 - Q1
```

The IQR shows how spread out the middle 50% of the data is.

A **box plot** shows:

- median,
- Q1,
- Q3,
- spread,
- possible outliers.

Box plots are useful for comparing groups, such as:

- cost by package type,
- margin by destination,
- rating by membership,
- stay length by travel month.

---

## How statistics can mislead

Statistics are useful, but they can be misleading if used without context.

Examples:

- Using the mean when the median would be more honest.
- Ignoring outliers.
- Hiding sample size.
- Comparing groups unfairly.
- Using charts that exaggerate differences.
- Treating correlation as causation.

A good analysis should use the statistic that fits the question and should explain the context.

---

## Simple EDA workflow

A good EDA process looks like this:

1. **Understand the goal**  
   Decide what question you want to answer.

2. **Understand the columns**  
   Know what each variable means.

3. **Identify data types**  
   Decide which columns are numeric, categorical, binary, or ordinal.

4. **Check data quality**  
   Look for missing values, impossible values, duplicates, and outliers.

5. **Calculate useful summaries**  
   Use mean, median, mode, quartiles, and counts where appropriate.

6. **Visualize the data**  
   Use charts like box plots to see patterns and outliers.

7. **Interpret carefully**  
   Ask whether the result actually answers the question.

8. **Connect to decisions**  
   Use the analysis to support pricing, marketing, customer strategy, or product decisions.

---

## Key takeaways

- EDA means understanding data before using it for decisions or machine learning.
- Different data types need different analysis methods.
- The mean is useful but sensitive to outliers.
- The median is better for skewed data.
- The mode is useful for categories and most-common-value questions.
- Outliers can be mistakes or important rare cases.
- Quartiles and IQR describe spread.
- Box plots show center, spread, and possible outliers.
- Statistics need context, or they can mislead.
- Good analysis starts with a clear question.
