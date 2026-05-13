
# Scaling Issues

If features are on different scales (e.g., meters vs centimeters),  
distance becomes dominated by large-scale features.

![[Pasted image 20260227090607.png|697]]

---

# Fixing Scaling Issues

## Standardization

$$\Large
x_{i,\text{std}} =
\frac{x_i - \mu_i}{\sigma_i}
$$

Zero mean, unit variance per feature.

---

## Mahalanobis Distance

$$\Large
d(x_1, x_2)
=
\sqrt{(x_1 - x_2)^T \Sigma^{-1} (x_1 - x_2)}
$$

If

$$\Large
\Sigma =
\begin{bmatrix}
\sigma_1^2 & 0 & \dots \\
0 & \ddots & 0 \\
\dots & 0 & \sigma_n^2
\end{bmatrix}
$$

then Mahalanobis equals Euclidean on normalized data.

---

# Curse of Dimensionality

1D input space:

$$\Large
x \in \{1, 2, \dots, 10\}
$$

For $N=20$ uniformly distributed samples → 100% coverage.

2D:

$$\Large
x \in \{1, \dots, 10\}^2
$$

Coverage ≈ 18%.

3D:

Coverage ≈ 2%.

![[Pasted image 20260226172209.png|697]]

Key consequences:

- Nearest neighbor becomes far away  
- Required $N$ grows exponentially with dimension  

---
# Links
[[Machine Learning]]