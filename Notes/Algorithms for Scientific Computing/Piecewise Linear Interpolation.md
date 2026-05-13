# Piecewise Linear Interpolation

Piecewise linear interpolation connects data points using straight-line segments.

Instead of one complicated global function, we use many local functions.

---

# Hat Functions

The basis functions are triangular "hat functions":

$$\Large
\phi_k(x)
=
\begin{cases}
\frac{x-x_{k-1}}{h_{k-1}}
&
x_{k-1}<x<x_k
\\
\\
\frac{x_{k+1}-x}{h_k}
&
x_k<x<x_{k+1}
\\
\\
0
&
\text{otherwise}
\end{cases}
$$

where:

$$
h_k = x_{k+1}-x_k
$$

---

# Key Property

Each hat function satisfies:

$$\Large
\phi_k(x_k)=1
$$

and:

$$\Large
\phi_k(x_n)=0
\quad \text{for } n\ne k
$$

This means every basis function only affects nearby points.

---

# Consequence

The interpolation coefficients become trivial:

$$\Large
c_k=f_k
$$

because each basis function isolates one grid point.

---

# Why Piecewise Linear Functions are Useful

Compared to high-degree polynomials:

- easier to compute
- numerically stable
- local support
- easy to adapt locally

---

# Intuition

Each basis function contributes a small triangular bump.

Adding many bumps together reconstructs the signal.

---
# Links
[[Interpolation]]
[[Algorithms for Scientific Computing]]