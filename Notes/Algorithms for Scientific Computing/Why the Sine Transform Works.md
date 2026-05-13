# Why the Sine Transform Works

The DST works because sine waves are eigenfunctions of the second derivative operator.

---

# Continuous Perspective

Consider:

$$\Large
-u''(x)=f(x)
$$

Suppose:

$$
u(x)=\sin(kx)
$$

Then:

$$
u''(x)=-k^2\sin(kx)
$$

Therefore:

$$\Large
-u''(x)=k^2\sin(kx)
$$

The sine function remains unchanged except for scaling.

---

# Eigenfunction Property

Functions that keep their shape under an operator are called eigenfunctions.

Sine functions are eigenfunctions of:

$$
\frac{d^2}{dx^2}
$$

---

# Discrete Analogue

The discrete operator:

$$\Large
-u_{n-1}+2u_n-u_{n+1}
$$

behaves similarly.

Its eigenvectors are discrete sine waves.

---

# Consequence

Applying the DST diagonalizes the matrix.

Instead of solving one large coupled system, we solve many tiny independent equations.

This is the mathematical reason the fast Poisson solver works.

---
# Links
[[Algorithms for Scientific Computing]]