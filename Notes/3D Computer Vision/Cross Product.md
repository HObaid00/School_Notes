# Cross Product

The **cross product** is an operation defined for two vectors in $\mathbb{R}^3$:

$$\Large
\times : \mathbb{R}^3 \times \mathbb{R}^3 \rightarrow \mathbb{R}^3
$$

Given two vectors

$$
u =
\begin{pmatrix}
u_1 \\
u_2 \\
u_3
\end{pmatrix},
\qquad
v =
\begin{pmatrix}
v_1 \\
v_2 \\
v_3
\end{pmatrix},
$$

their cross product is:

$$\Large
u \times v =
\begin{pmatrix}
u_2v_3 - u_3v_2 \\
u_3v_1 - u_1v_3 \\
u_1v_2 - u_2v_1
\end{pmatrix}
$$

The result $u \times v$ is a vector that is perpendicular to both $u$ and $v$.

The cross product is **anti-commutative**:

$$\Large
u \times v = - v \times u
$$

This means the order matters. Swapping the input vectors flips the direction of the result.

Geometrically, the length of the cross product equals the area of the parallelogram spanned by $u$ and $v$:

$$\Large
|u \times v| = |u| |v| \sin(\theta)
$$

where $\theta$ is the angle between the two vectors.

Example:

If

$$
u =
\begin{pmatrix}
1 \\
0 \\
0
\end{pmatrix},
\qquad
v =
\begin{pmatrix}
0 \\
1 \\
0
\end{pmatrix},
$$

then

$$\Large
u \times v =
\begin{pmatrix}
0 \\
0 \\
1
\end{pmatrix}
$$

This follows the right-hand rule.

---

## Links

[[3D Computer Vision]]