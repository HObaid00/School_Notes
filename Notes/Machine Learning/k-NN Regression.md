# Definition

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
# 3-NN
![[Pasted image 20260427125421.png]]

---
# 1-NN
![[Pasted image 20260427125456.png]]

---
# Choosing k

Goal: good generalization.

Since future data is unavailable:

Split dataset $D$ into:

- Training set $D_T$
- Validation set $D_V$
- Test set $D_t$

![[Pasted image 20260427125604.png]]

Procedure:

1. Train model on training set
2. Evaluate different $k$ on validation set
3. Select best $k$
4. Report final performance on test set

![[Pasted image 20260226172038.png|697]]
Example: choose $k = 7$.

---
# Links
[[Machine Learning]]
