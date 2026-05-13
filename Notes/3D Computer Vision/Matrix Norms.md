# Matrix Norms

## Purpose of Matrix Norms

Matrix norms measure the "size" or "strength" of a matrix.

---

## Induced 2-Norm

The induced norm measures maximum stretching:

$$\Large ||A||_2 = \max_{||x||_2=1} ||Ax||_2$$

This equals the largest singular value:

$$\Large ||A||_2 = \sigma_1$$

---

## Frobenius Norm

The Frobenius norm sums all squared entries:

$$\Large ||A||_F = \sqrt{\sum_{i,j} a_{ij}^2}$$

Equivalent form:

$$\Large ||A ||_2 = \sigma_1,\quad ||A||_F = \sqrt{\text{trace}(A^TA)} = \sqrt{\sigma_1^2 + \dots+ \sigma_n^2}$$

---

## Interpretation

- Spectral norm → maximum amplification
- Frobenius norm → total energy

---

## Applications

Matrix norms appear in:

- Optimization
- Numerical analysis
- Machine learning
- Error estimation
- Regularization

---
[[3D Computer Vision]]
