# Notation

| Symbol                 | Meaning                                    |
| ---------------------- | ------------------------------------------ |
| $\Large s$             | scalar (lowercase, not bold)               |
| $\Large \mathbf{s}$    | vector (lowercase, bold)                   |
| $\Large \mathbf{S}$    | matrix (uppercase, bold)                   |
| $\Large \hat{y}$       | predicted class label                      |
| $\Large y$             | actual class label                         |
| $\Large \mathbb{I}(a)$ | Indicator function (1 if $a$ true, else 0) |

---
# Linear Classification

Linear classification is one of the most fundamental methods in machine learning.

The goal is to assign inputs to discrete categories.

Examples:

- spam vs non-spam emails
- cat vs dog image classification
- fraud detection
- disease diagnosis

---

# Classification vs Regression

## Regression

Regression predicts continuous values:

$$
y \in \mathbb{R}
$$

Example:

- predicting house prices

---

## Classification

Classification predicts discrete labels:

$$
y \in \{1,\dots,C\}
$$

Example:

- predicting whether an image contains a cat or a dog

---

# Classification Problem

We are given:

$$
D=\{(x_i,y_i)\}_{i=1}^{N}
$$

where:

- $x_i \in \mathbb{R}^D$ are feature vectors
- $y_i$ are class labels

The goal is to learn:

$$\Large
f:\mathbb{R}^D \rightarrow \mathcal{C}
$$

such that:

$$\Large
y_i=f(x_i)
$$

---

# Main Idea

A classifier divides the input space into regions corresponding to different classes.

---
# Links
[[Machine Learning]]