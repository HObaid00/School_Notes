# The Poisson Equation

The Poisson equation is one of the most important partial differential equations (PDEs) in scientific computing.

It appears in:

- heat transfer
- electrostatics
- fluid dynamics
- gravity
- image processing

---

# Continuous Form

In two dimensions:

$$\Large
-
k
\left(
\frac{\partial^2 T}{\partial x^2}
+
\frac{\partial^2 T}{\partial y^2}
\right)
=
f(x,y)
$$

where:

- $T(x,y)$ is the unknown temperature
- $f(x,y)$ represents heat sources
- $k$ is a material constant

---

# Physical Meaning

The equation describes equilibrium.

At equilibrium:

- heat entering a region
- equals heat leaving it
- plus internal heat generation

---

# Laplacian Operator

The expression:

$$\Large
\frac{\partial^2 T}{\partial x^2}
+
\frac{\partial^2 T}{\partial y^2}
$$

is called the **Laplacian**.

It measures how curved or uneven the temperature field is.

---

# Intuition

If one point is hotter than nearby points:

- heat flows outward
- smoothing the temperature

The Poisson equation describes this balancing process.

---

# Special Case: No Heat Sources

If:

$$
f(x,y)=0
$$

then the equation becomes:

$$\Large
\nabla^2 T = 0
$$

which is called **Laplace's Equation**.

---
# Links
[[Algorithms for Scientific Computing]]