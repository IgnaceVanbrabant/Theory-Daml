# Week 1 - Data Exploration: Meaningful Summary

Source: `Week_1_-_Data_Exploration_ce24.pdf`  
Course: Data Analytics & Machine Learning  
Topic: Exploratory Data Analysis (EDA)

This summary groups the lecture into the main ideas you need to understand, with selected pictures from the PDF where they help explain the concept.

---

## 1. The big idea of this lesson

![Overview of the week](assets/week-1-data-exploration/slide-02.jpg)

The first week is about learning how to understand data before trying to use it for AI or machine learning. This step is called **Exploratory Data Analysis**, or **EDA**.

EDA is important because data is not automatically useful. A dataset can contain many columns, different data types, mistakes, extreme values, and patterns that are not obvious at first. Before building models or making decisions, we need to know what the data represents and how reliable it is.

The lecture focuses on four main ideas:

1. **Understand the business case.**  
   Data should be connected to a real problem or decision.

2. **Recognize data types.**  
   Different kinds of data need different statistics, charts, and model treatment.

3. **Use summary statistics carefully.**  
   Numbers like the mean, median, and mode summarize data, but each one answers a different question.

4. **Do not trust statistics without context.**  
   A statistic can be correct mathematically but still give a misleading impression.

---

## 2. The case study: Ada Lovelace's travel agency

The lecture uses a fictional travel agency as the running example. This makes the theory easier to understand because every data column can be connected to a business meaning.

![Travel agency dataset columns](assets/week-1-data-exploration/slide-07.jpg)

The dataset contains information such as:

| Column | Meaning | Why it matters |
| --- | --- | --- |
| `SalesID` | Unique sale identifier | Helps track individual transactions. |
| `Age` | Customer age | Can reveal customer groups or market segments. |
| `Country` | Customer country | Useful for regional demand analysis. |
| `Membership` | Standard, silver, or gold membership | May show loyalty or customer value. |
| `Previous_Purchases` | Past purchases | Helps measure returning-customer behavior. |
| `Package type` | Relaxation, cultural, or adventure | Shows what type of product was sold. |
| `Destination` | Travel destination | Helps identify popular locations. |
| `Cost` | Price or cost-related value | Important for revenue and pricing decisions. |
| `Margin` | Profit margin | Shows how profitable a sale or package is. |
| `Guests` | Number of travelers | Affects package size and total value. |
| `Stay_length` | Length of the trip | Can influence cost, margin, and customer satisfaction. |
| `Travel_month` | Month of travel | Useful for seasonality and demand patterns. |
| `Earlybird discount` | Whether a discount was used | Helps evaluate promotions. |
| `Rating` | Customer rating | Measures satisfaction. |

The important point is that these columns are not just random data. They describe customers, products, money, travel behavior, discounts, and satisfaction. EDA helps turn these raw columns into useful knowledge.

---

## 3. Good analysis starts with questions

![Example business questions](assets/week-1-data-exploration/slide-08.jpg)

The lecture gives examples of questions we can ask with the travel-agency data:

- What package type are we selling the most?
- Which package type has the highest cost?
- Which package type has the highest margin?
- Can historical data help us choose prices instead of doing it manually?

These questions are important because they decide what kind of analysis is needed.

For example:

- **Selling the most** means we need counts or frequencies.
- **Highest cost** means we need numeric comparison.
- **Highest margin** means we need profitability analysis.
- **Choosing prices using historical data** moves toward prediction and decision-making.

A common mistake is to calculate statistics without first knowing the question. EDA should start with purpose: what do we want to learn, and what decision could this support?

---

## 4. Data types: why they matter so much

A central part of the lecture is learning data types. This matters because the data type determines what operations make sense.

You cannot analyze every column in the same way. A country, a rating, a cost, and a membership level all behave differently.

### 4.1 Continuous numeric data

![Continuous numeric data](assets/week-1-data-exploration/slide-09.jpg)

**Continuous numeric data** can take many possible values, including decimal values. In the PDF, `Cost` is used as an example.

Examples:

- cost,
- margin,
- price,
- distance,
- temperature,
- time.

For this kind of data, calculations like mean, median, minimum, maximum, range, and standard deviation can make sense.

However, continuous values still need rules. For example, cost should normally be positive. If a travel package has a negative cost, the number might be an error or it might need special explanation.

### 4.2 Discrete numeric data

**Discrete numeric data** is numeric, but it can only take specific values. A rating from 1 to 5 is a good example.

Examples:

- customer rating: 1, 2, 3, 4, or 5,
- number of guests,
- number of previous purchases,
- stay length measured in whole days.

Discrete data can be counted. Sometimes averages are useful, but we must remember that the average may create a value that does not exist. For example, an average rating of 4.3 summarizes the group, but no individual customer may have given exactly 4.3.

### 4.3 Nominal categorical data

**Nominal categorical data** contains categories with no natural order.

Examples:

- country,
- destination,
- package type,
- payment method.

A nominal category can be encoded as a number, but the number is only a label. If Belgium = 1, France = 2, and Germany = 3, that does not mean Germany is greater than France in a mathematical way. This is especially important in machine learning, where a bad encoding can make a model learn fake relationships.

### 4.4 Binary data

![Binary data](assets/week-1-data-exploration/slide-12.jpg)

**Binary data** has only two possible values.

Examples:

- paid or unpaid,
- discount or no discount,
- member or non-member,
- cancelled or not cancelled.

Binary data is often stored as true/false or 1/0. This is useful because it is easy to count and filter. But the meaning of the 1 and 0 must always be clear.

### 4.5 Ordinal categorical data

![Ordinal categorical data](assets/week-1-data-exploration/slide-13.jpg)

**Ordinal categorical data** has categories with a meaningful order.

Example from the PDF:

```text
Standard < Silver < Gold
```

This order matters: gold is higher than silver, and silver is higher than standard. But the distance between categories may not be equal. The step from standard to silver might not represent the same business value as the step from silver to gold.

That is why ordinal data must be handled carefully. It has order, but it is not always a true measurement scale.

---

## 5. Summary statistics: reducing a lot of data into useful information

A dataset can contain too many rows to inspect manually. Summary statistics help capture important parts of the data in a few numbers.

The lecture focuses on:

- mean,
- median,
- mode,
- outliers,
- Q1 and Q3,
- box plots.

Each one answers a different question.

---

## 6. Mean: useful, but easy to misunderstand

![Average legs example](assets/week-1-data-exploration/slide-18.jpg)

The lecture uses the statement:

> The average human has less than 2 legs.

This sounds strange because most humans have 2 legs. But it is mathematically possible because some people have fewer than 2 legs. When all values are added together and divided by the number of people, the result becomes slightly less than 2.

The mean is calculated as:

```text
mean = sum of all values / number of values
```

### What the mean does well

The mean gives a quick central value for numeric data. It is useful for questions like:

- What is the average cost of a package?
- What is the average margin?
- What is the average rating?
- What is the average stay length?

### What the mean does badly

The mean is sensitive to extreme values. One very high value or very low value can pull the average away from what is typical.

So the mean answers:

> What is the arithmetic balance point?

It does **not** always answer:

> What is most common or typical?

That distinction is one of the most important lessons in the PDF.

---

## 7. Median: better for skewed data and outliers

![Why use the median](assets/week-1-data-exploration/slide-24.jpg)

The **median** is the middle value after sorting the data.

If the data is skewed or has outliers, the median can describe the typical case better than the mean.

The PDF gives an example similar to income:

```text
[10, 10, 10, 10, 10, 10, 50, 300]
```

Most values are close to 10, but 300 is much larger. The mean will be pulled upward by 300. The median stays closer to the middle of the actual data.

### Why this matters

In the travel-agency dataset, the median may be better than the mean for:

- package cost,
- margin,
- stay length,
- number of previous purchases,
- customer spending.

If a few luxury trips are extremely expensive, the average cost may look high even though most customers buy cheaper trips. The median helps show what a typical customer experiences.

---

## 8. Mode: the most common value

![Mode explanation](assets/week-1-data-exploration/slide-31.jpg)

The **mode** is the value that appears most often.

This is especially useful for categorical data, because mean and median often do not make sense for categories.

Examples of mode questions:

- What is the most common package type?
- What is the most common destination?
- Which membership level appears most often?
- What rating is given most often?
- Which country has the most customers?

The mode answers a different question than the mean or median. It tells us what is most frequent, not what is mathematically central.

---

## 9. Outliers: strange values that need investigation

![Outliers explanation](assets/week-1-data-exploration/slide-26.jpg)

Outliers are values that differ strongly from the rest of the data.

They can happen because of:

- measurement errors,
- typing mistakes,
- unit mistakes,
- rare but real events,
- unusual customers or products.

For example, if a trip cost is recorded as 100000 instead of 1000, it may be a typing error. But a very expensive luxury trip could also be real. That is why outliers should not be deleted automatically.

### Why outliers matter

Outliers can strongly affect analysis:

- They can pull the mean up or down.
- They can make graphs harder to read.
- They can hide the normal pattern.
- They can reveal important rare cases.
- They can indicate data-quality problems.

Good EDA investigates outliers instead of ignoring them.

---

## 10. How statistics can mislead

![Statistics can mislead](assets/week-1-data-exploration/slide-28.jpg)

The lecture includes the quote:

> There are 3 kinds of lies: lies, damned lies, and statistics.

The point is not that statistics are useless. The point is that statistics can be used in misleading ways.

A statistic can mislead when someone:

- reports only the mean while hiding outliers,
- chooses a chart scale that exaggerates differences,
- ignores sample size,
- compares groups unfairly,
- hides missing data,
- presents correlation as if it proves causation,
- chooses the statistic that supports the desired story.

For example, saying "the average package cost is high" might be true because of a few luxury packages. But if most customers buy cheaper packages, the median gives a different and important part of the story.

A meaningful analysis should usually compare multiple summaries instead of relying on only one number.

---

## 11. Q1, Q3, IQR, and box plots

![Box plot components](assets/week-1-data-exploration/slide-38.jpg)

The lecture introduces Q1, Q3, and box plots as tools for understanding distribution.

### Q1 and Q3

- **Q1** is the first quartile, around the 25% point.
- **Q3** is the third quartile, around the 75% point.

Together, they show the middle 50% of the data.

### IQR

The **interquartile range** is:

```text
IQR = Q3 - Q1
```

It measures how spread out the middle half of the data is.

### Box plots

A box plot summarizes a distribution visually:

- The line inside the box shows the median.
- The bottom of the box shows Q1.
- The top of the box shows Q3.
- The box height shows the IQR.
- The whiskers show spread outside the box.
- Points beyond the whiskers can indicate outliers.

The lecture notes that whiskers can stretch up to 1.5 times the IQR. Values beyond that range are often treated as possible outliers.

### Why box plots are useful

Box plots are useful because they show center, spread, skew, and possible outliers in one compact visual.

For the travel-agency data, box plots could compare:

- cost by package type,
- margin by package type,
- rating by membership level,
- stay length by destination,
- cost by travel month.

This is better than only comparing averages, because the box plot also shows whether the values are stable, spread out, or affected by outliers.

---

## 12. A good EDA workflow for this dataset

![The point of summary statistics](assets/week-1-data-exploration/slide-42.jpg)

The lecture ends with the idea that we have too much data to inspect everything manually. The goal is to capture the "essence" of the data using a few meaningful numbers and visuals.

A good EDA workflow for the travel-agency dataset would be:

1. **Understand the goal.**  
   Decide what question you want to answer, such as profitability, popularity, customer satisfaction, or pricing.

2. **Identify the relevant columns.**  
   For profitability, use columns like `Cost`, `Margin`, `Package type`, and `Destination`.

3. **Classify the data types.**  
   Know which columns are numeric, categorical, binary, or ordinal.

4. **Check data quality.**  
   Look for missing values, impossible values, duplicates, wrong units, and strange outliers.

5. **Calculate the right summaries.**  
   Use mean and median for numeric data, mode for categorical data, and quartiles for spread.

6. **Visualize important patterns.**  
   Use charts such as box plots to compare groups and detect unusual values.

7. **Interpret carefully.**  
   Ask whether the statistic actually answers the business question.

8. **Connect the result to a decision.**  
   Use the analysis to support pricing, marketing, product design, or customer strategy.

---

## 13. Most important takeaways

- EDA is the process of understanding data before using it for decisions or machine learning.
- The same column can be mathematically simple but business-wise important.
- Data types determine which statistics and charts make sense.
- Continuous data, discrete data, nominal categories, binary data, and ordinal categories must be treated differently.
- The mean is useful, but it is sensitive to extreme values.
- The median is often better for skewed data or data with outliers.
- The mode is the best basic summary for many categorical questions.
- Outliers should be investigated, not blindly removed.
- Q1, Q3, and IQR describe the spread of the middle part of the data.
- Box plots summarize center, spread, and possible outliers in one visual.
- Statistics can mislead if they are presented without context.
- Good analysis uses the right statistic for the right question.

---

## 14. Quick reference table

| Concept | Best used for | What it answers | Watch out for |
| --- | --- | --- | --- |
| Mean | Numeric data | What is the arithmetic average? | Can be distorted by outliers. |
| Median | Numeric data, skewed data | What is the middle value? | Does not show full spread by itself. |
| Mode | Categorical or repeated values | What occurs most often? | There can be multiple modes. |
| Outlier | Data-quality and unusual-case checks | Which values are strange? | Strange does not always mean wrong. |
| Q1 and Q3 | Numeric distributions | Where is the middle 50%? | Need sorted data or percentile calculation. |
| IQR | Spread of numeric data | How wide is the middle 50%? | Does not describe all extreme values. |
| Box plot | Comparing distributions | What are the center, spread, and outliers? | Needs interpretation; not every point is shown. |

