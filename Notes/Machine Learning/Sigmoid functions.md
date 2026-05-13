# Sigmoid Function

The sigmoid function converts arbitrary real numbers into probabilities.

---

# Definition

$$\Large
\sigma(a)
=
\frac1{1+e^{-a}}
$$

---

# Output Range

The sigmoid maps:

$$\Large
(-\infty,\infty)
\rightarrow
(0,1)
$$

---

# Interpretation

- large positive input $\rightarrow$ probability near 1
- large negative input $\rightarrow$ probability near 0

---

# Example

$$\Large
\sigma(0)=0.5
$$

$$\Large
\sigma(10)\approx1
$$

$$\Large
\sigma(-10)\approx0
$$

---

# Why It Matters

Sigmoid allows linear models to output probabilities instead of hard decisions.

---
# Links
[[Machine Learning]]