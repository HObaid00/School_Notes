# Discrete Poisson Equation

After discretization, the continuous PDE becomes a linear system.

---

# 1D Version

The lecture studies:

$$\Large
-u_{n-1}
+
2u_n
-
u_{n+1}
=
f_n
$$

for:

$$
n=1,\dots,N-1
$$

with boundary conditions:

$$\Large
u_0=u_N=0
$$

---

# Interpretation

- $u_n$ = unknown solution values
- $f_n$ = forcing term
- neighboring values influence each other

Each equation connects nearby grid points.

---

# Matrix Form

The system can be written as:

$$\Large
Au=f
$$

where:

$$
A=
\begin{bmatrix}
2 & -1 & 0 & \cdots \\
-1 & 2 & -1 & \cdots \\
0 & -1 & 2 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{bmatrix}
$$

This is called a **tridiagonal matrix**.

---

# Why It Becomes Difficult

In 2D:

- the matrix becomes huge
- direct solution methods become expensive

Example:

$$
1000\times1000
$$

grid points produce millions of unknowns.

Efficient algorithms become essential.

---
# Links
[[Algorithms for Scientific Computing]]