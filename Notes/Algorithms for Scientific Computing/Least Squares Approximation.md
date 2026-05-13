# Least Squares Approximation

Real-world data is often noisy.

Instead of exact interpolation, we compute the best approximation.

---

# Approximation Model

Represent the function as:

$$\Large
f_N(x)
=
\sum_{j=1}^{N}
v_j\phi_j(x)
$$

where:

- $\phi_j(x)$ are basis functions
- $v_j$ are unknown coefficients

---

# Approximation Error

For training points:

$$
(x_i,y_i)
$$

the prediction error is:

$$
f_N(x_i)-y_i
$$

---

# Least Squares Objective

We minimize the total squared error:

$$\Large
\sum_{i=1}^{m}
(f_N(x_i)-y_i)^2
\to
\min
$$

---

# Matrix Form

Define:

$$\Large
G_{ij}=\phi_j(x_i)
$$

Then the problem becomes:

$$\Large
\|Gv-y\|^2
\to
\min
$$

---

# Normal Equations

Taking derivatives leads to:

$$\Large
G^T G v
=
G^T y
$$

This is the classical least-squares system.

---

# Why Squared Errors?

Squaring:

- penalizes large errors strongly
- produces smooth optimization problems
- leads to linear algebra formulations

---

# Interpretation

Least squares finds the function that best fits all data points simultaneously.

---
# Links
[[Least Squares]]
[[Minsta Kvadrat Metoden (MK)|Least Square Error (LSE)]]
[[Algorithms for Scientific Computing]]
