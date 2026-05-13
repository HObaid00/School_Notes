# Homogeneous Coordinates

Homogeneous coordinates allow rotations and translations to be written as one matrix multiplication.

A normal 3D point is:

$$\Large
X =
\begin{pmatrix}
X_1 \\
X_2 \\
X_3
\end{pmatrix}
$$

In homogeneous coordinates, we write:

$$\Large
\bar{X}
=
\begin{pmatrix}
X_1 \\
X_2 \\
X_3 \\
1
\end{pmatrix}
$$

A rigid-body transformation is represented as:

$$\Large
g =
\begin{pmatrix}
R & T \\
0 & 1
\end{pmatrix}
$$

Then:

$$\Large
\bar{X}' = g\bar{X}
$$

Expanding the multiplication gives:

$$\Large
\begin{pmatrix}
X' \\
1
\end{pmatrix}
=
\begin{pmatrix}
R & T \\
0 & 1
\end{pmatrix}
\begin{pmatrix}
X \\
1
\end{pmatrix}
=
\begin{pmatrix}
RX + T \\
1
\end{pmatrix}
$$

So homogeneous coordinates let us write:

$$\Large
X' = RX + T
$$

as one linear-looking matrix equation.

This is especially useful in computer vision, robotics, and graphics, where many coordinate transformations must be concatenated.

---

## Links

[[3D Computer Vision]]