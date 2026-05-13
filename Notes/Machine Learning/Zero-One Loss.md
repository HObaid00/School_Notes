# Zero-One Loss

To evaluate a classifier, we count how many predictions are wrong.

---

# Prediction

Let:

$$\Large
\hat{y}_i=f(x_i)
$$

be the predicted label.

---

# Zero-One Loss

The zero-one loss is:

$$\Large
\ell_{01}(y,\hat{y})
=
\sum_{i=1}^{N}
I(\hat{y}_i \ne y_i)
$$

where:

$$\Large
I(a)=
\begin{cases}
1 & \text{if } a \text{ is true}\\
0 & \text{otherwise}
\end{cases}
$$

---

# Interpretation

Each misclassified sample contributes:

$$\Large
1
$$

Each correctly classified sample contributes:

$$\Large
0
$$

---

# Example

Suppose:

| True | Predicted |
|---|---|
| Cat | Cat |
| Dog | Cat |
| Dog | Dog |

Only one prediction is wrong.

Therefore:

$$\Large
\ell_{01}=1
$$

---

# Limitation

Although intuitive, zero-one loss is difficult to optimize directly because it is not smooth.

---
# Links
[[Machine Learning]]