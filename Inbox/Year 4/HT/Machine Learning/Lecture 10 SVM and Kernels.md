**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning Group  
Technical University of Munich  
Winter Term 2025/2026  

---

# Roadmap

1. Support Vector Machines (SVM)  
2. Soft Margin SVM  
3. Kernels  

---

# Section 1: Support Vector Machines (SVM)

## Linear Classifier

A linear classifier assigns:

- Class +1 if  
  $$\Large
  w^T x + b > 0
  $$
- Class −1 if  
  $$\Large
  w^T x + b < 0
  $$

Prediction:

$$\Large
h(x) = \text{sign}(w^T x + b)
$$

with

$$\Large
\text{sign}(z) =
\begin{cases}
-1 & z < 0 \\
0 & z = 0 \\
+1 & z > 0
\end{cases}
$$

---

# Maximum Margin Classifier

Goal: Find a hyperplane that separates the classes with **maximum margin**.

Motivation:

- Larger margin → better generalization (Statistical Learning Theory, Vapnik 1995)

---

## Linear Classifier with Margin

Add two parallel hyperplanes:

For class +1:
$$\Large
w^T x + b \ge 1
$$

For class −1:
$$\Large
w^T x + b \le -1
$$

Unified constraint:

$$\Large
y_i (w^T x_i + b) \ge 1
$$

---

## Size of the Margin

Signed distance from origin to hyperplane:

$$\Large
d = -\frac{b}{\|w\|}
$$

Margin:

$$\Large
m = \frac{2}{\|w\|}
$$

Thus maximizing margin ≡ minimizing $\|w\|$.

---

# SVM Primal Optimization Problem

Given training data $(x_i, y_i)$ with $y_i \in \{-1, 1\}$:

$$\Large
\min_{w,b} \frac{1}{2} w^T w
$$

subject to

$$\Large
y_i (w^T x_i + b) \ge 1
$$

This is a **convex quadratic programming problem**.

---

# Constrained Optimization & Lagrangian

General problem:

$$\Large
\min_\theta f_0(\theta)
$$

subject to

$$\Large
f_i(\theta) \le 0
$$

Lagrangian:

$$\Large
L(\theta, \alpha)
=
f_0(\theta)
+
\sum_{i=1}^M \alpha_i f_i(\theta)
$$

with $\alpha_i \ge 0$.

---

# Dual Formulation

Dual function:

$$\Large
g(\alpha)
=
\min_\theta L(\theta, \alpha)
$$

Dual problem:

$$\Large
\max_\alpha g(\alpha)
$$

subject to:

$$\Large
\alpha_i \ge 0
$$

Strong duality holds for convex SVM problem.

---

# SVM Dual Problem

After derivation:

$$\Large
\max_\alpha
\sum_{i=1}^N \alpha_i
-
\frac{1}{2}
\sum_{i=1}^N
\sum_{j=1}^N
\alpha_i \alpha_j y_i y_j x_i^T x_j
$$

subject to

$$\Large
\sum_{i=1}^N \alpha_i y_i = 0
$$

$$\Large
\alpha_i \ge 0
$$

This is a quadratic programming (QP) problem.

---

# Recovering Parameters

Weights:

$$\Large
w = \sum_{i=1}^N \alpha_i y_i x_i
$$

Bias:

For any support vector $x_i$ with $\alpha_i > 0$:

$$\Large
b = y_i - w^T x_i
$$

---

# Support Vectors

From complementary slackness:

$$\Large
\alpha_i [y_i(w^T x_i + b) - 1] = 0
$$

Thus:

- $\alpha_i \ne 0$ only if point lies on margin.
- Such points are **support vectors**.

Classification:

$$\Large
h(x)
=
\text{sign}
\left(
\sum_{i \in S}
\alpha_i y_i x_i^T x + b
\right)
$$

Sparse solution: only support vectors matter.

---

# Section 2: Soft Margin SVM

## Handling Non-Separable Data

Introduce slack variables $\xi_i \ge 0$.

Relaxed constraint:

$$\Large
y_i(w^T x_i + b) \ge 1 - \xi_i
$$

New objective:

$$\Large
\min_{w,b,\xi}
\frac{1}{2} w^T w
+
C \sum_{i=1}^N \xi_i
$$

- $C > 0$ controls penalty.
- $C \to \infty$ → hard margin.

![[Pasted image 20260228182056.png|697]]

---

# Dual with Slack Variables

Dual becomes:

$$\Large
\max_\alpha
\sum_{i=1}^N \alpha_i
-
\frac{1}{2}
\sum_{i=1}^N
\sum_{j=1}^N
\alpha_i \alpha_j y_i y_j x_i^T x_j
$$

subject to

$$\Large
\sum_{i=1}^N \alpha_i y_i = 0
$$

$$\Large
0 \le \alpha_i \le C
$$

New constraint: $\alpha_i \le C$.

---

# Influence of C

- Large $C$: small margin, fewer misclassifications
- Small $C$: larger margin, more violations

![[Pasted image 20260228182908.png]]

---

# Hinge Loss Formulation

Slack variables at optimum:

$$\Large
\xi_i = \max(0, 1 - y_i(w^T x_i + b))
$$

Thus objective becomes:

$$\Large
\min_{w,b}
\frac{1}{2} w^T w
+
C
\sum_{i=1}^N
\max(0, 1 - y_i(w^T x_i + b))
$$

Hinge loss:

$$\Large
E_{\text{hinge}}(z) = \max(0, 1 - z)
$$

Convex approximation of zero-one loss.

---

# Section 3: Kernels

## Feature Space Mapping

We can map data:

$$\Large
\phi: \mathbb{R}^D \to \mathbb{R}^M
$$

Example:

$$\Large
\phi(x,y)
=
\begin{pmatrix}
x \\
y \\
-\sqrt{x^2 + y^2}
\end{pmatrix}
$$
![[Pasted image 20260228183300.png|697]]

---

# Kernel Trick

In dual, data only appears as inner products:

$$\Large
x_i^T x_j
$$

Define kernel:

$$\Large
k(x_i, x_j)
=
\phi(x_i)^T \phi(x_j)
$$

Dual becomes:

$$\Large
\max_\alpha
\sum_{i=1}^N \alpha_i
-
\frac{1}{2}
\sum_{i,j}
\alpha_i \alpha_j y_i y_j k(x_i, x_j)
$$

---

# Kernelized Classification

$$\Large
h(x)
=
\text{sign}
\left(
\sum_{j \in S}
\alpha_j y_j k(x_j, x)
+
b
\right)
$$

---

# Valid Kernels

Kernel must produce symmetric positive semidefinite Gram matrix:

$$\Large
K_{ij} = k(x_i, x_j)
$$

(Mercer’s theorem)

---

# Kernel-Preserving Operations

If $k_1, k_2$ are kernels:

- $k_1 + k_2$
- $c k_1$ with $c>0$
- $k_1 k_2$
- $x_1^T A x_2$ with PSD $A$

are also kernels.

---

# Common Kernels

## Linear
$$\Large
k(a,b) = a^T b
$$

## Polynomial
$$\Large
k(a,b) = (a^T b)^p
$$
or
$$\Large
(a^T b + 1)^p
$$

## Gaussian (RBF)
$$\Large
k(a,b)
=
\exp\left(
-\frac{\|a-b\|^2}{2\sigma^2}
\right)
$$

## Sigmoid
$$\Large 
k(a,b) = \tanh(\kappa a^T b - \delta)
$$

---

![[Pasted image 20260228183352.png|697]]

---

# Hyperparameter Selection

Tune:

- $C$
- Kernel parameters ($\sigma$, $\gamma$, $p$, etc.)

Use:

- Cross-validation
- Random search

![[Pasted image 20260228183412.png]]

---

# Multi-Class SVM

Standard SVM is binary.

Strategies:

## One-vs-Rest
Train $C$ classifiers.

## One-vs-One
Train $\binom{C}{2}$ classifiers.

---

# Summary

- SVM maximizes margin.
- Convex optimization → global optimum.
- Dual formulation → quadratic programming.
- Soft margin handles noise.
- Hinge loss allows gradient-based optimization.
- Kernel trick enables nonlinear decision boundaries.
- Works only in dual formulation.