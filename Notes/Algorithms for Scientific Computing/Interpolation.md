Meaning Introduced or inserted, in the context of Fourier Series and Scientific Computing, Interpolation means to derive the two function that made the combined function. 

---
# Definition
**Given:
* a set of values: $\Large f_i, \ f_{ij},  \dots \ \text{(1D, 2D, ...)}$
* at grid/sampling points $\Large x_i, \ x_{ij}, \ \dots$
**Wanted:
* function $\Large f(x) = \sum a_i \phi_i(x)$ such that $\Large f(x_i) = f_i$ (similar in 2D)
* we need to compute the coefficients $\Large a_i$
**Important aspects:
* solution depends on clever choice of the basis functions $\Large \phi_i$ (recall: Lagrange/Newton interpolation)
* can we skip coefficients/basis functions a-priori/a-posteriori?
>	adaptivity, compression, etc.

---
## Recall: Interpolation Problem
For given values $b_i$ and points $x_i$ ($i=1, \ \dots \ , \ n$) find a function $f(x)$, such that:
$$\Large
f(x_i) = b_i \ \forall \ i = 1, \ ..., \ n \quad \text{where} f(x_i) = \sum_{j=1}^n \ a_j \ g_j(x_i) 
$$
The functions $g_j(x)(j=1, \ \dots, \ n)$ are suitably selected (polynomials, e.g.).

With $G_{ij} := g_j(x_i)$, we can write the problem as a system of linear equations:
$$\Large
\begin{array}a
\sum_{j=1}^n \ a_j g_j(x_i) = n_i \forall \ i=1, \ \dots, \ n \\
\iff \sum_{j=1}^n \ G_{ij}a_j \forall \ i=1, \ \dots, \ n
\end{array}
$$
Corresponds to solving a linear system of equations: $\Large Ga \ = \ b$
