## Approximation of Data
**Given:
* a set of values: $f_i, \ f_i{ij}, \ \dots$ (1D, 2D, ...)
* at points $x_i, x_{ij}, \ \dots$
**Wanted:
* function $f(x) = \sum a_i \phi_i(x)$ such that $\sum (f_i - f(x_i))^2$ is minimal
* we need to compute the coefficient $a_i$
**Important aspects:
* typically more data $f_i$ than coefficients (overdetermined)
* solution depends on clever of the basis function $\phi_i$ -> how many functions, and how should they look like?
* related to classification and learning("big data")

---
## Recall: Approximation Problem

For given values $b_i$ and points $x_i$ $(i = 1, \dots, m)$ find a function $f(x)$, such that:

$$\Large
f(x_i) \approx b_i \quad \text{for all } i = 1, \dots, m
$$

where

$$\Large
f(x_i) = \sum_{j=1}^{n} a_j g_j(x_i), \quad \text{with } m > n
$$

---

We find the best approximation by minimising the quadratic error:

$$\Large
\sum_{i=1}^{m} (f(x_i) - b_i)^2 \; \overset{!}{=} \; \min
\;\;\Longleftrightarrow\;\;
\sum_{i=1}^{m} \left( \sum_{j=1}^{n} a_j g_j(x_i) - b_i \right)^2 \; \overset{!}{=} \; \min
$$

---

We set all derivatives w.r.t. our variables $a_k$ to $0$  
(with $G_{ij} := g_j(x_i)$ for all $k = 1, \dots, n$):

$$\Large
\frac{\partial}{\partial a_k}
\left(
\sum_{i=1}^{m}
\left( \sum_{j=1}^{n} a_j G_{ij} - b_i \right)^2
\right)
=
\sum_{i=1}^{m}
\frac{\partial}{\partial a_k}
\left( \sum_{j=1}^{n} a_j G_{ij} - b_i \right)^2
\overset{!}{=} 0
$$

$$\Large
\Longleftrightarrow
\sum_{i=1}^{m}
2 \left( \sum_{j=1}^{n} a_j G_{ij} - b_i \right) G_{ik} = 0
$$

$$\Large
\Longleftrightarrow
\sum_{i=1}^{m} G_{ik} \sum_{j=1}^{n} a_j G_{ij}
=
\sum_{i=1}^{m} G_{ik} b_i
$$

---

Corresponds to solving a linear system of equations:
$$\Large
G^T G a = G^T b
$$
---
