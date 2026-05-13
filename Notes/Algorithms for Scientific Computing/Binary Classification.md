# Binary Classification

Binary classification assigns one of two labels to data points.

Examples:

- spam or not spam
- fraud or legitimate
- survived or not survived
- yes or no

---

# Mathematical Setup

Each data point is:

$$
\vec{x}\in\mathbb{R}^d
$$

where:

- $d$ is the number of features

Examples of features:

- age
- income
- height
- purchase history

---

# Labels

Binary labels are represented as:

$$\Large
K=\{+1,-1\}
$$

For example:

| Label | Meaning |
|---|---|
| +1 | positive class |
| -1 | negative class |

---

# Training Set

The classifier learns from labeled examples:

$$\Large
S=
\{
(\vec{x}_i,y_i)
\}_{i=1}^m
$$

where:

- $\vec{x}_i$ = feature vector
- $y_i$ = known class label

---

# Goal

Learn a function:

$$
f(\vec{x})
$$

that predicts labels for new unseen data.

---

# Prediction Rule

After constructing an approximation:

$$
f_N(\vec{x})
$$

classify using:

$$\Large
f_N(\vec{x}) \ge 0
\Rightarrow +1
$$

otherwise:

$$\Large
f_N(\vec{x}) < 0
\Rightarrow -1
$$

---

# Main Idea

Classification builds a decision boundary separating different classes.

---
# Links
[[Algorithms for Scientific Computing]]