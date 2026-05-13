# Binary Cross Entropy Loss

Logistic regression is trained using maximum likelihood estimation.

---

# Likelihood

For independent samples:

$$\Large
p(y|w,X)
=
\prod_{i=1}^{N}
\sigma(w^Tx_i)^{y_i}
(1-\sigma(w^Tx_i))^{1-y_i}
$$

---

# Negative Log-Likelihood

Taking the negative logarithm gives:

$$\Large
E(w)
=
-\sum_{i=1}^{N}
\left[
y_i\log\sigma(w^Tx_i)
+
(1-y_i)\log(1-\sigma(w^Tx_i))
\right]
$$

---

# Binary Cross Entropy

This loss is called:

$$\Large
\text{binary cross entropy}
$$

---

# Intuition

The loss heavily penalizes confident wrong predictions.

---

# Optimization

Unlike linear regression, logistic regression has no closed-form solution.

Optimization methods like gradient descent are used instead.

---
# Links
[[Machine Learning]]
