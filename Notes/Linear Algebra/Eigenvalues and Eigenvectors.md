# Eigenvalues and Eigenvectors

## Core Idea

An eigenvector keeps its direction after transformation.

If:

$$\Large Av = \lambda v$$

then:

- $v$ is an eigenvector
- $\lambda$ is the eigenvalue

---

## Interpretation

The matrix transforms the vector only by scaling.

- $|\lambda|>1$ → stretching
- $|\lambda|<1$ → shrinking
- Negative $\lambda$ → direction flip

---

## Characteristic Equation

Eigenvalues satisfy:

$$\Large
|\lambda I - A| = 0$$

This polynomial is called the characteristic polynomial.

## Properties
- $\text{tr}(A) = \sum \lambda_i$
- $|A| = \prod \lambda_i$



---

## Symmetric Matrices

Symmetric matrices have special properties:

1. Real eigenvalues
2. Orthogonal eigenvectors
3. Orthogonal diagonalization

---

## Diagonalization

A symmetric matrix can be written as:

$$\Large A = V\Lambda V^T$$

where:

- $V$ contains eigenvectors
- $\Lambda$ contains eigenvalues

---

## Why Eigenvalues Matter

Eigenanalysis is used in:

- PCA
- Stability analysis
- Quantum mechanics
- Vibrations
- Spectral graph theory
- Machine learning

---
# Links
[[Linear Algebra]]
[[3D Computer Vision]]