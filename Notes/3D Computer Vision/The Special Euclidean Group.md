# The Special Euclidean Group $SE(3)$

The group $SE(3)$ represents rigid-body motions in 3D, including both rotation and translation.

An element of $SE(3)$ is:

$$\Large
g = (R,T)
$$

where:

$$
R \in SO(3),
\qquad
T \in \mathbb{R}^3
$$

The transformation of a point is:

$$\Large
X' = RX + T
$$

Using homogeneous coordinates, we write this as a $4 \times 4$ matrix:

$$\Large
g =
\begin{pmatrix}
R & T \\
0 & 1
\end{pmatrix}
\in SE(3)
$$

A 3D point is written in homogeneous form as:

$$\Large
\bar{X}
=
\begin{pmatrix}
X \\
1
\end{pmatrix}
$$

Then the rigid-body motion becomes a single matrix multiplication:

$$\Large
\bar{X}' = g\bar{X}
$$

The group $SE(3)$ is called the **special Euclidean group**.

Important distinction:

- Points in $\mathbb{E}^3$ can be rotated and translated.
- Free vectors in $\mathbb{R}^3$ are only rotated, not translated.

This is because a vector represents direction and magnitude, not absolute position.

---
