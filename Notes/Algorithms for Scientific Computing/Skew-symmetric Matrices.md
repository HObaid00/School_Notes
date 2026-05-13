# Skew-Symmetric Matrices

## Definition

A matrix is skew-symmetric if:

$$\Large A^T = -A$$

This means:

- Diagonal entries are zero
- Upper triangle is negative lower triangle

---

## 3D Cross Product Matrix

For:

$$\Large u=(u_1,u_2,u_3)^T$$

its hat matrix is:

$$\Large
\hat{u}=
\begin{bmatrix}
0 & -u_3 & u_2 \\
u_3 & 0 & -u_1 \\
-u_2 & u_1 & 0
\end{bmatrix}
$$

---

## Cross Product Representation

The hat matrix satisfies:

$$\Large \hat{u}v = u \times v$$

This converts cross products into matrix multiplication. For $u \not= 0$, we have $\text{rank} (\hat u) = 2$ and the null space of $\hat u$ is spanned by $u$, because $\hat u u = u^\top \hat u = 0$ 

---

## Properties

Skew-symmetric matrices:

- Have purely imaginary eigenvalues
- Have even rank
- Represent rotations infinitesimally

---

## Applications

They are heavily used in:

- Robotics
- Rigid-body motion
- Lie groups
- Computer vision
- Rotational dynamics

---
# Links
[[3D Computer Vision]]