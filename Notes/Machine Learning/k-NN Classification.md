# Definition

More robust than 1-NN.

Let $N_k(x)$ be the $k$ nearest neighbors of $x$.

Class probability:

$$\Large
p(y = c \mid x, k) =
\frac{1}{k}
\sum_{i \in N_k(x)} \mathbb{I}(y_i = c)
$$

Prediction:

$$\Large
\hat{y} = \arg\max_c p(y = c \mid x, k)
$$

with the *Indicator* variable $\mathbb{I}(e)$ is defined as:

$$\Large
\mathbb{I}(e) =
\begin{cases}
1 & \text{if } e \text{ is true} \\
0 & \text{otherwise}
\end{cases}
$$

The vector is labeled by the **mode** of its neighbors’ labels.

---
# Weighted k-NN Classification

Weight neighbors inversely proportional to distance.

$$\Large
p(y = c \mid x, k)
=
\frac{1}{Z}
\sum_{i \in N_k(x)}
\frac{1}{d(x, x_i)}
\mathbb{I}(y_i = c)
$$

where

$$\Large
Z =
\sum_{i \in N_k(x)}
\frac{1}{d(x, x_i)}
$$

Prediction:

$$\Large
\hat{y} = \arg\max_c p(y = c \mid x, k)
$$

---
# Links
[[Machine Learning]]
