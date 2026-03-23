**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
Winter Term 2025/2026  

---

# Iris Dataset

![[Pasted image 20260226171453.png|697]]

---

## Iris Dataset: 2 Features

Features shown:

- petal_length  
- petal_width  
- target ∈ {setosa, versicolor, virginica}

Intuition for labeling new samples:

> Look at the surrounding points.  
> Do as your neighbor does.

![[Pasted image 20260226171513.png|697]]

---

# 1-NN Algorithm

Given a training dataset

$$\Large
D = \{(x_i, y_i)\}_{i=1}^N
$$

where:

- $\Large x_i \in \mathbb{R}^D$ are features  
- $\Large y_i \in \{1, \dots, C\}$ are class labels  

To classify new observations:

1. Define a distance measure (e.g., Euclidean distance)
2. Compute the nearest neighbor for each new data point
3. Assign the label of the nearest neighbor

Works for both classification and regression.

---

## 1-NN and Voronoi Tessellation

1-NN induces a Voronoi tessellation of the space.

This often results in **poor generalization**.

![[Pasted image 20260226171608.png|697]]

---

# k-Nearest Neighbor Classification

More robust than 1-NN.

Let $N_k(x)$ be the $k$ nearest neighbors of $x$.

Class probability:

$$\Large
p(y = c \mid x, k) =
\frac{1}{k}
\sum_{i \in N_k(x)} \mathbb{I}(y_i = c)
$$

Prediction:

$$\Large
\hat{y} = \arg\max_c p(y = c \mid x, k)
$$

Indicator function:

$$\Large
\mathbb{I}(e) =
\begin{cases}
1 & \text{if } e \text{ is true} \\
0 & \text{otherwise}
\end{cases}
$$

The vector is labeled by the **mode** of its neighbors’ labels.

---

# Refresher: Discrete Probability

Example: Jar with balls {4 red, 10 green, 6 blue}

$$\Large
p(\text{red}) = \frac{4}{4+10+6} = \frac{4}{20} = 0.2
$$

Similarly:

- $\Large p(\text{green}) = 0.5$
- $\Large p(\text{blue}) = 0.3$

Properties of probability mass function:

- $\Large p(X=x) \ge 0$
- $\Large \sum_x p(X=x) = 1$

---

# Weighted k-NN Classification

Weight neighbors inversely proportional to distance.

$$\Large
p(y = c \mid x, k)
=
\frac{1}{Z}
\sum_{i \in N_k(x)}
\frac{1}{d(x, x_i)}
\mathbb{I}(y_i = c)
$$

where

$$\Large
Z =
\sum_{i \in N_k(x)}
\frac{1}{d(x, x_i)}
$$

Prediction:

$$\Large
\hat{y} = \arg\max_c p(y = c \mid x, k)
$$

---

# k-NN Regression

For regression:

$$\Large
\hat{y}
=
\frac{1}{Z}
\sum_{i \in N_k(x)}
\frac{1}{d(x, x_i)} y_i
$$

with

$$\Large
Z =
\sum_{i \in N_k(x)}
\frac{1}{d(x, x_i)}
$$

Here, $y_i \in \mathbb{R}$.

Prediction is a **weighted mean** of neighbors.

---

# Choosing k

Goal: good generalization.

Since future data is unavailable:

Split dataset $D$ into:

- Training set $D_T$
- Validation set $D_V$
- Test set $D_t$

Procedure:

1. Train model on training set
2. Evaluate different $k$ on validation set
3. Select best $k$
4. Report final performance on test set

![[Pasted image 20260226172038.png|697]]
Example: choose $k = 7$.

---

# Measuring Classification Performance

## Confusion Matrix

|               | Predicted 1 | Predicted 0 |
|---------------|------------|------------|
| True 1        | TP         | FN         |
| True 0        | FP         | TN         |

- TP = true positive  
- TN = true negative  
- FP = false positive  
- FN = false negative  

![[Pasted image 20260226172059.png]]

---

## Metrics

Accuracy:

$$\Large
\text{acc} = \frac{TP + TN}{TP + TN + FP + FN}
$$

Precision:

$$\Large
\text{prec} = \frac{TP}{TP + FP}
$$

Recall (Sensitivity):

$$\Large
\text{rec} = \frac{TP}{TP + FN}
$$

Specificity:

$$\Large
\text{tnr} = \frac{TN}{FP + TN}
$$

False Negative Rate:

$$\Large
\text{fnr} = \frac{FN}{TP + FN}
$$

False Positive Rate:

$$\Large
\text{fpr} = \frac{FP}{FP + TN}
$$

F1 Score:

$$\Large
\text{f1} =
\frac{2 \cdot \text{prec} \cdot \text{rec}}
{\text{prec} + \text{rec}}
$$

Note:

- Trade-off between precision and recall  
- Be careful with imbalanced classes  

---

# Distance Measures

Euclidean distance (L2):

$$\Large
d(u,v) =
\sqrt{\sum_i (u_i - v_i)^2}
$$

L1 norm:

$$\Large
d(u,v) =
\sum_i |u_i - v_i|
$$

L∞ norm:

$$\Large
d(u,v) =
\max_i |u_i - v_i|
$$

Angle (cosine similarity):

$$\Large
\cos \alpha =
\frac{u^T v}{\|u\| \|v\|}
$$

Mahalanobis distance:

$$\Large
d(u,v) =
\sqrt{(u-v)^T \Sigma^{-1} (u-v)}
$$

Other distances:

- Hamming distance  
- Edit distance  

---

# Scaling Issues

If features are on different scales (e.g., meters vs centimeters),  
distance becomes dominated by large-scale features.

![[Pasted image 20260227090607.png|697]]

---

# Fixing Scaling Issues

## Standardization

$$\Large
x_{i,\text{std}} =
\frac{x_i - \mu_i}{\sigma_i}
$$

Zero mean, unit variance per feature.

---

## Mahalanobis Distance

$$\Large
d(x_1, x_2)
=
\sqrt{(x_1 - x_2)^T \Sigma^{-1} (x_1 - x_2)}
$$

If

$$\Large
\Sigma =
\begin{bmatrix}
\sigma_1^2 & 0 & \dots \\
0 & \ddots & 0 \\
\dots & 0 & \sigma_n^2
\end{bmatrix}
$$

then Mahalanobis equals Euclidean on normalized data.

---

# Curse of Dimensionality

1D input space:

$$\Large
x \in \{1, 2, \dots, 10\}
$$

For $N=20$ uniformly distributed samples → 100% coverage.

2D:

$$\Large
x \in \{1, \dots, 10\}^2
$$

Coverage ≈ 18%.

3D:

Coverage ≈ 2%.

![[Pasted image 20260226172209.png|697]]

Key consequences:

- Nearest neighbor becomes far away  
- Required $N$ grows exponentially with dimension  

---

# Practical Considerations

k-NN is expensive:

- Memory: store entire training set  
- Inference: naive search is $O(N)$  

Solution:

- Use tree-based structures (e.g., k-d tree)  
- Approximate nearest neighbors  

---

# Summary

We covered:

- k-NN algorithm  
- Train-validation-test split  
- Classification metrics  
- Distance metrics  
- Scaling issues  
- Curse of dimensionality  

---

# Reading Material

Main:

- Murphy, *Machine Learning: A Probabilistic Perspective*  
  (Ch. 1.4.1 – 1.4.3)

Extra:

- Barber, *Bayesian Reasoning and Machine Learning*  
  (Ch. 14)

Slides adapted from previous versions by W. Koepp & D. Korhammer.