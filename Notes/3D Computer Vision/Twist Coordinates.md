# Twist Coordinates

A twist matrix $\hat{\xi} \in \mathfrak{se}(3)$ can be represented by a 6-dimensional vector.

The twist coordinates are:

$$\Large
\xi =
\begin{pmatrix}
v \\
w
\end{pmatrix}
\in \mathbb{R}^6
$$

where:

- $v \in \mathbb{R}^3$ represents linear velocity,
- $w \in \mathbb{R}^3$ represents angular velocity.

The hat operator maps twist coordinates to a matrix:

$$\Large
\xi^\wedge
=
\begin{pmatrix}
v \\
w
\end{pmatrix}^{\wedge}
=
\begin{pmatrix}
\hat{w} & v \\
0 & 0
\end{pmatrix}
\in \mathbb{R}^{4 \times 4}
$$

The vee operator maps the matrix back to vector form:

$$\Large
\left(
\begin{pmatrix}
\hat{w} & v \\
0 & 0
\end{pmatrix}
\right)^\vee
=
\begin{pmatrix}
v \\
w
\end{pmatrix}
$$

This is useful because:

- the matrix form $\hat{\xi}$ is convenient for exponentiation,
- the vector form $\xi$ is convenient for optimization and storage.

In robotics and computer vision, camera motion is often optimized using these 6 twist parameters.

---

## Links

[[The Lie Algebra of Twists]]
[[3D Computer Vision]]
