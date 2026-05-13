# Singular Value Decomposition (SVD)

## What is SVD?

The Singular Value Decomposition factorizes a matrix into:

$$\Large A = U\Sigma V^T$$

where:

- $U \in \mathbb R^{m\times n}$ contains left singular vectors (whose columns are orthonormal)
- $V \in \mathbb R ^{n \times p}$ contains right singular vectors (whose columns are orthonormal)
- $\Sigma \in \mathbb R^{p\times p}, \ \sigma = \text{diag}\{\sigma_1, \dots, \sigma_p \}$ contains singular values, where $\sigma_1 \ge \dots \ge \sigma_p$ 

---

## Why SVD Matters

SVD is one of the most important tools in linear algebra.

It works for:

- Square matrices
- Rectangular matrices
- Rank-deficient matrices

---

## Geometric Interpretation

SVD transforms space in three stages:

1. Rotate using $V^T$
2. Scale using $\Sigma$
3. Rotate using $U$

The unit sphere becomes an ellipsoid.

The singular values determine the axis lengths.

---

## Singular Values

Singular values are:

$$\Large \sigma_i = \sqrt{\lambda_i(A^TA)}$$

where $\lambda_i$ are eigenvalues.

---

## Rank and SVD

The number of nonzero singular values equals:

$$\Large \text{rank}(A)$$

---

## Applications

SVD is used in:

- PCA
- Image compression
- Noise reduction
- Least squares
- Recommendation systems
- Computer vision

---

## Low-Rank Approximation

Keeping only the largest singular values produces a compressed approximation:

$$\Large A \approx U_k \Sigma_k V_k^T$$

This is foundational in data compression.

---
# Links
[[Linear Algebra]]
[[Algorithms for Scientific Computing]]