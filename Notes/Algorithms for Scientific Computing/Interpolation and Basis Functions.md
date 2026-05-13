# Interpolation and Basis Functions

Interpolation means constructing a function that exactly matches known data points.

Suppose we know:

$$
(x_0,f_0), (x_1,f_1), \dots, (x_{N-1},f_{N-1})
$$

We want a function that passes through all these points.

---

# General Interpolation Formula

We choose basis functions:

$$
g_k(x)
$$

and represent the unknown function as:

$$\Large
f(x)
=
\sum_{k=0}^{N-1}
c_k g_k(x)
$$

The unknowns are the coefficients:

$$
c_k
$$

---

# Interpolation Condition

At every supporting point:

$$\Large
f_n
=
\sum_{k=0}^{N-1}
c_k g_k(x_n)
$$

This produces a system of equations for the coefficients.

---

# Why Basis Functions Matter

Different basis functions produce different approximation properties.

Examples:

| Basis Functions | Result |
|---|---|
| Polynomials | Polynomial interpolation |
| Sine/Cosine | Fourier methods |
| Piecewise linear | Local interpolation |

---

# Main Idea

Complex functions can be built from combinations of simple building blocks.

---
# Links
[[Basis and Linear Independence]]
[[Interpolation]]
[[Algorithms for Scientific Computing]]
