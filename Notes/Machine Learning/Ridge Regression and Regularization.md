# Ridge Regression and Regularization

Regularization helps prevent overfitting.

The idea is simple:

- penalize overly large weights

---

# Ridge Regression Loss

The ridge regression objective is:

$$\Large
E_{ridge}(w)
=
\frac12
\sum_{i=1}^{N}
(w^T\phi(x_i)-y_i)^2
+
\frac{\lambda}{2}\|w\|_2^2
$$

---

# L2 Penalty

The penalty term is:

$$\Large
\|w\|_2^2
=
w^Tw
=
\sum_j w_j^2
$$

---

# Meaning of $\lambda$

$$\lambda$$ controls regularization strength.

---

# Small $\lambda$

- flexible model
- risk of overfitting

---

# Large $\lambda$

- small weights
- smoother model
- risk of underfitting

---

# Intuition

Regularization discourages extreme parameter values.

This usually improves generalization.

![[Pasted image 20260506193829.png]]

---
# Links
[[Polynomial Degree]]
[[Machine Learning]]