# Velocity Transformation in Camera Coordinates

Let a world point $X_0$ be observed from a moving camera. Its camera-frame coordinates are:

$$\Large
X(t) = g(t)X_0
$$

Differentiating with respect to time gives:

$$\Large
\dot{X}(t)
=
\dot{g}(t)X_0
$$

Since:

$$\Large
X_0 = g^{-1}(t)X(t),
$$

we get:

$$\Large
\dot{X}(t)
=
\dot{g}(t)g^{-1}(t)X(t)
$$

Define the twist matrix:

$$\Large
\hat{V}(t)
=
\dot{g}(t)g^{-1}(t)
=
\begin{pmatrix}
\hat{w}(t) & v(t) \\
0 & 0
\end{pmatrix}
\in \mathfrak{se}(3)
$$

Then:

$$\Large
\dot{X}(t)
=
\hat{V}(t)X(t)
$$

In ordinary 3D coordinates, this becomes:

$$\Large
\dot{X}(t)
=
\hat{w}(t)X(t) + v(t)
$$

Since $\hat{w}X = w \times X$, we can also write:

$$\Large
\dot{X}(t)
=
w(t) \times X(t) + v(t)
$$

Interpretation:

- $w(t)$ describes angular velocity.
- $v(t)$ describes linear velocity.
- $\hat{V}(t)$ represents the relative velocity of the world frame as seen from the camera frame.

---

## Links

[[3D Computer Vision]]