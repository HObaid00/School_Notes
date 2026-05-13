# Regularized Logistic Regression

Like linear regression, logistic regression can overfit.

Regularization controls model complexity.

---

# Regularized Loss

$$\Large
E(w)
=
-\log p(y|w,X)
+
\lambda\|w\|_q^q
$$

---

# L2 Regularization

For:

$$
q=2
$$

we get ridge-style regularization:

$$\Large
\lambda\|w\|_2^2
$$

---

# Effect

Large weights are penalized.

This:

- reduces overfitting
- improves generalization
- stabilizes optimization

---

# Bayesian Interpretation

L2 regularization corresponds to MAP estimation with a Gaussian prior on $w$.

---
# Links
[[Machine Learning]]