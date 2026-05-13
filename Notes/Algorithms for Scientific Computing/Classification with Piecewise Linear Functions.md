# Classification with Piecewise Linear Functions

Instead of global polynomials, classification can use local piecewise linear basis functions.

---

# Advantages

Piecewise linear basis functions have:

- local support
- sparse matrices
- efficient computations

---

# System Matrix

Define:

$$\Large
G_{ij}=\phi_j(x_i)
$$

Because hat functions only affect nearby regions, most matrix entries are zero.

This produces a sparse matrix.

---

# Sparse Structure

The lecture shows that:

$$\Large
G^T G
$$

becomes tridiagonal.

This is extremely important computationally.

---

# Why Tridiagonal Matrices Matter

Tridiagonal systems can be solved efficiently in:

$$\Large
O(N)
$$

time.

---

# Challenges

Choosing grid resolution is difficult.

---

# Too Fine Resolution

If the grid is too fine:

- intervals may contain no data
- the model overfits noise

---

# Too Coarse Resolution

If the grid is too coarse:

- important patterns are lost
- approximation quality suffers

---

# Desired Property

We want:

- fine resolution where data is complicated
- coarse resolution where data is smooth

This motivates hierarchical methods.

---
# Links
[[Piecewise Linear Interpolation]]
[[Algorithms for Scientific Computing]]