# High-Dimensional Classification Example — Optidigits

The lecture discusses handwritten digit recognition.

This is a classic machine learning problem.

---

# Input Data

Each handwritten digit image is converted into:

$$\Large
64
$$

numerical features.

These features are grayscale values of image pixels.

---

# Binary Classifiers

Instead of directly recognizing all digits simultaneously, the method constructs:

$$\Large
10
$$

binary classifiers.

Each classifier answers:

- "Is this digit a 0?"
- "Is this digit a 1?"
- etc.

---

# One-vs-All Strategy

For digit $k$:

- class $+1$ means "digit is $k$"
- class $-1$ means "digit is not $k$"

---

# Why High Dimensions are Hard

The feature space is:

$$
\mathbb{R}^{64}
$$

This creates enormous computational challenges.

---

# Importance of Hierarchical Methods

Hierarchical and sparse-grid methods help reduce computational complexity.

Without dimensionality reduction or sparsity, many algorithms become impractical.

---

# Big Picture

This lecture connects:

- interpolation
- approximation theory
- numerical analysis
- machine learning
- high-dimensional data analysis

into one unified framework.

---
# Links
[[Algorithms for Scientific Computing]]