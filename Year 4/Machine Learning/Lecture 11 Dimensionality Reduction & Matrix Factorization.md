**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning Group  
Technical University of Munich  
Winter Term 2025/2026  

---

# Roadmap

1. Introduction  
2. Principal Component Analysis (PCA)  
3. Singular Value Decomposition (SVD)  
4. Matrix Factorization  
5. Neighbor Graph Methods  
6. Autoencoders (Non-linear Dimensionality Reduction)  

---

# 1. Introduction

## Supervised vs. Unsupervised Learning

- Supervised learning:  
  $$\Large
  y = f(x)
  \quad \text{or} \quad
  p(y \mid x)
  $$

- Unsupervised learning:  
  $$\Large
  p(x)
  $$

Latent-variable view:

- Assume latent variable $z$
- Generative model:
  $$\Large
  p(x) = \int p(x \mid z)\, p(z)\, dz
  $$

Examples:
- Clustering → latent state = cluster label  
- Anomaly detection → low $p(x)$  

---

## Dimensionality Reduction Motivation

High-dimensional data problems:

- Expensive similarity computations  
- Highly correlated features  
- Curse of dimensionality  
- Hard to visualize  

Often data lies on a low-dimensional manifold embedded in high-dimensional space.

Goal:

- Reduce dimensionality
- Preserve information
- Improve efficiency
- Reveal intrinsic dimensionality

---

## Feature Selection vs Transformation

Feature selection:
- Remove dimensions directly
- Ignores correlations

Better idea:
- Linear transformation (change of basis)

Let $F \in \mathbb{R}^{d \times k}$ orthonormal.

Transformation:

$$\Large
X' = X F
$$

Covariance transformation:

$$\Large
\Sigma_{X'} = F^T \Sigma_X F
$$

---

# 2. Principal Component Analysis (PCA)

## Goal

Find orthogonal transformation such that:

- New dimensions are uncorrelated
- Variance concentrated in first components

---

## Data Setup

Given:

$$\Large
X \in \mathbb{R}^{N \times d}
$$

Rows: data points  
Columns: dimensions  

Mean:

$$\Large
\bar{x} = \frac{1}{N} X^T \mathbf{1}
$$

Center data:

$$\Large
\tilde{x}_i = x_i - \bar{x}
$$

---

## Covariance Matrix

Variance:

$$\Large
\text{Var}(X_j)
=
\frac{1}{N}
\sum_{i=1}^N
(x_{ij} - \bar{x}_j)^2
$$

Covariance:

$$\Large
\text{Cov}(X_{j_1}, X_{j_2})
=
\frac{1}{N}
\sum_{i=1}^N
(x_{ij_1}-\bar{x}_{j_1})
(x_{ij_2}-\bar{x}_{j_2})
$$

Matrix form:

$$\Large
\Sigma_X
=
\frac{1}{N} X^T X
-
\bar{x}\bar{x}^T
$$

---

## Eigendecomposition

Since $\Sigma_X$ is symmetric:

$$\Large
\Sigma_X = \Gamma \Lambda \Gamma^T
$$

- $\Gamma$ = eigenvectors  
- $\Lambda$ = diagonal matrix of eigenvalues  

Principal components = eigenvectors.

Transformation:

$$\Large
Y = \tilde{X} \Gamma
$$

In new space:

- Covariances = 0  
- Variance in dimension $i$ = $\lambda_i$

---

## Dimensionality Reduction

Keep first $k$ eigenvectors:

$$\Large
Y_{reduced} = \tilde{X} \Gamma_k
$$

90% rule:

$$\Large
\sum_{i=1}^k \lambda_i
\ge
0.9 \sum_{i=1}^d \lambda_i
$$

---

## PCA Complexity

- Covariance computation: $O(N d^2)$  
- Eigendecomposition: $O(d^3)$  

Power iteration for largest eigenvector:

$$\Large
v \leftarrow \frac{A v}{\|A v\|}
$$

Convergence rate:

$$\Large
\frac{\lambda_2}{\lambda_1}
$$

---
![[Pasted image 20260228183631.png|697]]
![[Pasted image 20260228183647.png]]

---

# 3. Singular Value Decomposition (SVD)

## Definition

For any matrix $A \in \mathbb{R}^{n \times d}$:

$$\Large
A = U \Sigma V^T
$$

- $U \in \mathbb{R}^{n \times r}$  
- $V \in \mathbb{R}^{d \times r}$  
- $\Sigma$ diagonal  
- $r = \text{rank}(A)$  
- $\sigma_1 \ge \sigma_2 \ge \dots \ge 0$

Equivalent form:

$$\Large
A
=
\sum_{i=1}^r
\sigma_i u_i v_i^T
$$

---

## Low-Rank Approximation

Goal:

$$\Large
\min_{rank(B)=k}
\|A - B\|_F^2
$$

Best solution:

- Set smallest singular values to zero.

Energy rule:

$$\Large
\sum_{i=1}^k \sigma_i^2
\ge
0.9
\sum_{i=1}^r \sigma_i^2
$$

---

## Theorem (Best Approximation)

Let:

$$\Large
A = U \Sigma V^T
$$

Truncate to $k$ largest singular values:

$$\Large
B = U \Sigma_k V^T
$$

Then $B$ minimizes:

$$\Large
\|A - B\|_F
$$

---

## Projection

Projected data:

$$\Large
P = A V
$$

---

## PCA vs SVD

Centered data $X$:

$$\Large
X = U \Sigma V^T
$$

Covariance:

$$\Large
X^T X
=
V \Sigma^2 V^T
$$

Thus:

- PCA eigenvectors = right singular vectors  
- Eigenvalues = squared singular values  

PCA and SVD are equivalent (for centered data).

---

# 4. Matrix Factorization (Recommender Systems)

## Netflix Prize Motivation

- 100M ratings  
- 480k users  
- 17k movies  
- Evaluation: RMSE  

$$\Large
RMSE
=
\sqrt{
\frac{1}{|S|}
\sum_{(u,i)\in S}
(r_{ui} - \hat{r}_{ui})^2
}
$$

---

## Problem with Classical SVD

- Missing entries treated as 0  
- Not appropriate for recommender systems  
- Dense singular vectors  
- Orthogonality unnecessary  

---

## Latent Factor Model

Find:

$$\Large
Q \in \mathbb{R}^{n \times k}, \quad
P \in \mathbb{R}^{d \times k}
$$

Minimize:

$$\Large
\min_{Q,P}
\sum_{(u,i)\in S}
(r_{ui} - q_u^T p_i)^2
$$

Prediction:

$$\Large
\hat{r}_{ui} = q_u^T p_i
$$

No orthogonality constraint.

---

# 5. Neighbor Graph Methods

(High-level overview)

Goal:

- Preserve local neighborhood structure  
- Examples:
  - Isomap  
  - LLE  
  - Laplacian Eigenmaps  

![[Pasted image 20260228183731.png|697]]

---

# 6. Autoencoders (Non-linear DR)

Neural network:

Encoder:
$$\Large
z = f_\theta(x)
$$

Decoder:
$$\Large
\hat{x} = g_\phi(z)
$$

Minimize reconstruction loss:

$$\Large
\|x - \hat{x}\|^2
$$

Can capture nonlinear manifolds.

---

# Summary

- PCA: diagonalize covariance  
- SVD: optimal low-rank approximation  
- PCA ≡ SVD (centered data)  
- Matrix factorization handles missing data  
- Neighbor graph methods preserve locality  
- Autoencoders enable nonlinear dimensionality reduction