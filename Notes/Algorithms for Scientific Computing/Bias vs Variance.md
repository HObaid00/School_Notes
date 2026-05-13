# Bias–Variance Tradeoff

Prediction error comes from two major sources:

- bias
- variance

---

# Bias

Bias measures systematic error.

High bias means:

- model too simple
- fails to capture true structure

Example:

- fitting a straight line to a curved function

---

# Variance

Variance measures sensitivity to training data.

High variance means:

- model changes dramatically with small data changes
- model captures noise

---

# Tradeoff

Usually:

- reducing bias increases variance
- reducing variance increases bias

---

# High Bias Example

Strong regularization:

$$
\lambda \gg 1
$$

creates rigid models.

---

# High Variance Example

Weak regularization:

$$
\lambda \approx 0
$$

allows unstable highly flexible models.

---

# Goal

Find a balance:

- low bias
- low variance

This is one of the central ideas in machine learning.

![[Pasted image 20260506193956.png]]

---
# Links
[[Machine Learning]]
