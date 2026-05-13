# Skew-Symmetric Matrices and the Hat Operator

For a vector

$$
u =
\begin{pmatrix}
u_1 \\
u_2 \\
u_3
\end{pmatrix}
\in \mathbb{R}^3,
$$

we can build a skew-symmetric matrix using the **hat operator**:

$$\Large
\hat{u}
=
\begin{pmatrix}
0 & -u_3 & u_2 \\
u_3 & 0 & -u_1 \\
-u_2 & u_1 & 0
\end{pmatrix}
$$

This matrix is called **skew-symmetric** because:

$$\Large
\hat{u}^\top = -\hat{u}
$$

The hat matrix represents the cross product as matrix multiplication:

$$\Large
\hat{u}v = u \times v
$$

This is useful because it turns the nonlinear-looking cross product operation into a linear matrix operation with respect to $v$.

The set of all $3 \times 3$ skew-symmetric matrices is called $\mathfrak{so}(3)$:

$$\Large
\mathfrak{so}(3)
=
\{ \hat{u} \mid u \in \mathbb{R}^3 \}
$$

There is also an inverse operation called the **vee operator**:

$$\Large
(\hat{u})^\vee = u
$$

So:

- $\wedge$ turns a vector into a skew-symmetric matrix.
- $\vee$ turns a skew-symmetric matrix back into a vector.

This connection is fundamental for representing rotations using Lie algebras.

---

## Links

[[3D Computer Vision]]