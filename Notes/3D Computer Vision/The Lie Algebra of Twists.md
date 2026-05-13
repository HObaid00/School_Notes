# The Lie Algebra of Twists

The Lie algebra of $SE(3)$ is called $\mathfrak{se}(3)$.

It describes infinitesimal rigid-body motions, which combine:

- infinitesimal rotation,
- infinitesimal translation.

A continuous rigid-body motion is written as:

$$\Large
g(t)
=
\begin{pmatrix}
R(t) & T(t) \\
0 & 1
\end{pmatrix}
\in SE(3)
$$

The corresponding velocity-like quantity is:

$$\Large
\dot{g}(t)g^{-1}(t)
$$

This has the form:

$$\Large
\dot{g}(t)g^{-1}(t)
=
\begin{pmatrix}
\hat{w}(t) & v(t) \\
0 & 0
\end{pmatrix}
$$

This matrix is called a **twist** and is denoted:

$$\Large
\hat{\xi}(t)
=
\begin{pmatrix}
\hat{w}(t) & v(t) \\
0 & 0
\end{pmatrix}
$$

Here:

- $w(t) \in \mathbb{R}^3$ is the angular velocity,
- $v(t) \in \mathbb{R}^3$ is the linear velocity.

The Lie algebra is:

$$\Large
\mathfrak{se}(3)
=
\left\{
\hat{\xi}
=
\begin{pmatrix}
\hat{w} & v \\
0 & 0
\end{pmatrix}
\mid
\hat{w} \in \mathfrak{so}(3),\ v \in \mathbb{R}^3
\right\}
$$

Intuition:

A twist is the infinitesimal version of a rigid-body transformation.

---

## Links

[[3D Computer Vision]]