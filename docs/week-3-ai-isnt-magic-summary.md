# Week 3 - AI Is Not Magic Summary

Source: `Week_3_-_AI_isn_t_magic_1__8737.pdf`  
Topic: Supervised learning, classification, regression, and basic models

## Main idea

Week 3 introduces machine learning as a practical way to learn patterns from existing data and use those patterns to make predictions.

The key idea is:

> AI is not magic. It uses data, variables, algorithms, and assumptions to make predictions.

This week focuses on:

- machine learning paradigms,
- supervised learning,
- classification,
- regression,
- K-Nearest Neighbors,
- decision trees,
- random forests,
- linear regression,
- logistic regression,
- thresholds,
- regularization.

---

## Machine learning paradigms

Machine learning can be split into different types depending on the kind of task and data.

The most important type in this lesson is **supervised learning**.

In supervised learning, the model learns from examples where the correct answer is already known.

Example:

| Input data | Known answer |
| --- | --- |
| customer age, salary, loan history | trustworthy or risky |
| package type, destination, stay length | expected cost |
| weather, temperature, humidity | play tennis or not |

The model uses the input data to learn patterns that connect variables to the target.

---

## Predictors and target

In supervised learning, there are two important parts:

### Predictor variables

Predictor variables are the input features used to make a prediction.

Examples:

- age,
- salary,
- country,
- membership level,
- previous purchases,
- package type,
- travel month.

These are often written as:

```text
x1, x2, ..., xp
```

### Target variable

The target variable is what we want to predict.

Examples:

- whether someone will repay a loan,
- how many months someone will pay on time,
- whether a tumor is malignant,
- how much a travel package will cost.

The target is often written as:

```text
y
```

---

## Classification vs regression

Supervised learning has two main prediction types: **classification** and **regression**.

### Classification

Classification predicts a category or class.

Examples:

- trustworthy or risky,
- spam or not spam,
- sick or healthy,
- will buy or will not buy,
- relaxation, cultural, or adventure package.

Use classification when the target is discrete.

### Regression

Regression predicts a numeric value.

Examples:

- cost of a trip,
- number of months someone pays on time,
- expected margin,
- customer rating,
- house price.

Use regression when the target is continuous or numeric.

### Main difference

| Task | Target type | Example question |
| --- | --- | --- |
| Classification | Category | Will this customer repay the loan? |
| Regression | Number | How many months will they pay on time? |

---

## Common supervised learning techniques

The lecture lists several models for classification and regression.

Classification examples:

- K-Nearest Neighbors,
- Naive Bayes,
- decision tree,
- random forest,
- support vector machines,
- logistic regression,
- artificial neural network.

Regression examples:

- linear regression,
- non-linear regression,
- K-Nearest Neighbors regression,
- decision tree regression,
- support vector regression,
- artificial neural network regression.

Different models work better for different problems. The right model depends on the data, the target, the amount of data, and how much interpretability is needed.

---

## K-Nearest Neighbors

**K-Nearest Neighbors**, or **KNN**, predicts a new instance by looking at the most similar known examples.

KNN is called an **instance-based** method because it uses stored training examples directly.

It is also called a **lazy learner** because training does almost nothing. The real work happens when a prediction is needed.

### How KNN works

1. Store the training data.
2. Receive a new unknown instance.
3. Find the `K` closest known instances.
4. Use those neighbors to predict the answer.

For classification:

- use the most common class among the neighbors.

For regression:

- use an average of the neighbors' numeric values.

---

## Choosing K in KNN

The value of **K** decides how many neighbors are used.

### K = 1

The model uses only the closest neighbor.

Advantage:

- very specific to the nearest example.

Problem:

- sensitive to noise or unusual data points.

### K greater than 1

The model uses multiple neighbors and usually takes the majority class.

Advantage:

- more stable.

Problem:

- if K is too large, the model may include neighbors that are not really similar.

### Ties

If K creates a tie, for example 2 green and 2 red, the model needs a rule to decide.

Possible tie solutions:

- choose an odd K,
- use distance-weighted voting,
- choose the class of the closest neighbor.

---

## Measuring similarity in KNN

KNN depends heavily on how similarity is measured.

Common distance measures:

| Distance | Best for | Main idea |
| --- | --- | --- |
| Hamming distance | Binary features | Count how many values are different |
| Euclidean distance | Continuous features | Straight-line distance |
| Manhattan distance | Grid-like data | Distance using horizontal and vertical steps |
| Chebyshev distance | Grid-like data with diagonals | Largest single-axis difference |

Choosing the wrong distance measure can make KNN predictions bad.

Example:

- For binary gene-mutation data, Hamming distance can make sense.
- For plant measurements, Euclidean distance can make sense.
- For movement on a grid, Manhattan or Chebyshev distance can make sense.

---

## Distance-weighted KNN

Normal KNN treats all selected neighbors equally.

Distance-weighted KNN gives closer neighbors more influence.

The idea is:

```text
closer neighbor = more important
farther neighbor = less important
```

One common method is to use inverse distance:

```text
weight = 1 / distance
```

This helps when close neighbors should clearly matter more than far-away neighbors.

---

## Decision trees

A **decision tree** is a model that makes predictions by splitting data into smaller groups.

It looks like a tree structure:

- **root node**: first split,
- **internal nodes**: later splits,
- **edges**: connections between nodes,
- **leaf nodes**: final predictions.

### How a decision tree works

1. Start with all training data.
2. Choose the best feature to split on.
3. Split the data into groups.
4. Keep splitting until a stopping rule is reached.
5. Predict based on the final leaf node.

Decision trees are useful because they are easy to understand. You can often follow the path of decisions and see why a prediction was made.

---

## Good splits in decision trees

The goal of a split is to make the lower nodes more **pure**.

A pure node means the examples in that node mostly belong to the same class.

Example:

- bad split: both child nodes are still very mixed,
- good split: one child node is mostly class A and the other is mostly class B.

Common split metrics:

- entropy,
- information gain,
- Gini index.

---

## Entropy

**Entropy** measures how mixed a group is.

Low entropy:

- the group is pure,
- most or all examples are from one class.

High entropy:

- the group is mixed,
- the classes are spread out.

For decision trees, lower entropy is better after a split.

---

## Information gain

**Information gain** measures how much entropy decreases after a split.

Formula idea:

```text
information gain = entropy before split - entropy after split
```

A good split gives high information gain because it makes the groups cleaner.

Decision trees often choose the split with the best information gain.

---

## Gini index

The **Gini index** measures how likely it is that an instance would be classified incorrectly if labeled randomly according to the class distribution.

Low Gini:

- purer group,
- better split.

High Gini:

- more mixed group,
- worse split.

Decision trees can use Gini index to choose splits. The best split is usually the one with the lowest Gini after splitting.

---

## ID3 algorithm

The lecture mentions ID3 as a decision-tree-building algorithm.

Simple idea:

1. Start with the training data.
2. If all instances have the same class, stop.
3. Otherwise, evaluate possible feature splits.
4. Choose the best split.
5. Split the data into subgroups.
6. Repeat the process for each subgroup.

This builds the tree step by step.

---

## Random forests

A **random forest** combines many decision trees into one model.

The idea is similar to the wisdom of the crowd:

- one person's guess may be wrong,
- many people's average guess is often better.

For random forests:

- one tree may be weak or inaccurate,
- many trees together usually make better predictions.

### How random forests make predictions

For classification:

- each tree votes for a class,
- the majority class wins.

For regression:

- each tree predicts a number,
- the forest averages the predictions.

---

## Why random forests work well

Each tree in a random forest is trained with randomness:

- random subset of rows,
- random subset of features.

This makes the trees different from each other.

That diversity helps reduce overfitting.

**Overfitting** means a model learns the training data too closely and performs badly on new data.

Random forests are often stronger than a single decision tree because they are more robust.

---

## Linear regression

**Linear regression** predicts a continuous numeric value.

Simple linear regression uses one predictor:

```text
y = beta0 + beta1 * X + error
```

Multiple linear regression uses multiple predictors:

```text
y = beta0 + beta1*x1 + beta2*x2 + ... + betap*xp + error
```

### What the parts mean

- `y`: value we want to predict,
- `x`: predictor variable,
- `beta0`: intercept,
- `beta1`, `beta2`, etc.: coefficients,
- `error`: noise or unexplained variation.

Linear regression is useful when the target is numeric, such as cost, margin, price, or time.

---

## Logistic regression

Despite the name, **logistic regression** is mainly used for classification.

It predicts the probability that an instance belongs to a class.

Example:

```text
P(y = 1) = probability that the instance is positive
```

Examples:

- probability that a customer is risky,
- probability that a tumor is malignant,
- probability that someone will play tennis,
- probability that a customer will buy.

---

## From linear to logistic regression

Linear regression can output any number, including values below 0 or above 1.

That is a problem for classification because probabilities must stay between 0 and 1.

Logistic regression solves this by using the **sigmoid function**.

The sigmoid function maps any real number to a value between 0 and 1.

This output can be interpreted as a probability.

---

## Thresholds in logistic regression

Logistic regression outputs a probability.

To turn that probability into a class, we use a **threshold**.

Example:

```text
if probability >= 0.5 -> predict class 1
if probability < 0.5 -> predict class 0
```

The threshold can be changed depending on the situation.

### Why thresholds matter

Changing the threshold changes the types of mistakes the model makes.

Example:

If a model predicts whether a tumor is cancerous, missing a real cancer case is very dangerous. In that case, you may choose a threshold that catches more possible cancers, even if it creates more false alarms.

Threshold choice depends on the cost of different errors.

---

## Regularization

**Regularization** helps prevent models from becoming too complex.

The idea:

> Simpler models often generalize better to new data.

Regularization adds a penalty for large or unnecessary coefficients.

This can reduce overfitting and make the model focus on the most useful variables.

### Lasso regression

Lasso adds a penalty based on the absolute size of coefficients.

Effect:

- can shrink some coefficients to zero,
- can remove less useful variables,
- works like feature selection.

### Ridge regression

Ridge adds a penalty based on squared coefficients.

Effect:

- shrinks coefficients,
- usually keeps all variables,
- reduces the influence of less useful variables.

---

## Simple Week 3 workflow

1. **Define the prediction target**  
   Decide what you want to predict.

2. **Decide whether the task is classification or regression**  
   Use classification for categories and regression for numbers.

3. **Choose predictor variables**  
   Select the features that may help predict the target.

4. **Prepare the data**  
   Clean missing values, encode categories, and scale variables if needed.

5. **Choose a model**  
   Examples: KNN, decision tree, random forest, linear regression, logistic regression.

6. **Train the model**  
   Let the model learn from known examples.

7. **Make predictions**  
   Use the model on new instances.

8. **Evaluate the model**  
   Check whether predictions are good enough. This becomes more important in the next lesson.

9. **Watch for overfitting**  
   A model should work on new data, not only on the training data.

---

## Key takeaways

- Supervised learning uses examples with known answers.
- Predictor variables are the inputs; the target is what we predict.
- Classification predicts categories.
- Regression predicts numeric values.
- KNN predicts based on similar known examples.
- Choosing K and the distance measure is important in KNN.
- Decision trees split data into purer groups.
- Entropy, information gain, and Gini index help choose tree splits.
- Random forests combine many decision trees for stronger predictions.
- Linear regression predicts continuous numeric values.
- Logistic regression predicts probabilities for classification.
- Thresholds turn probabilities into class predictions.
- Threshold choice depends on which mistakes are more costly.
- Regularization helps reduce overfitting and model complexity.
- AI models are not magic; they are structured methods for learning from data.
