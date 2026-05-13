# Lie-Cartan Coordinates

Lie-Cartan coordinates are coordinate systems for Lie groups built from the Lie algebra.

Given a basis of the Lie algebra $\mathfrak{so}(3)$:

$$\Large
(\hat{w}_1,\hat{w}_2,\hat{w}_3)
$$

we can define coordinates of the first kind by:

$$\Large
\alpha :
(\alpha_1,\alpha_2,\alpha_3)
\mapsto
\exp(
\alpha_1\hat{w}_1
+
\alpha_2\hat{w}_2
+
\alpha_3\hat{w}_3
)
$$

These use one exponential of a linear combination of basis elements.

Coordinates of the second kind are:

$$\Large
\beta :
(\beta_1,\beta_2,\beta_3)
\mapsto
\exp(\beta_1\hat{w}_1)
\exp(\beta_2\hat{w}_2)
\exp(\beta_3\hat{w}_3)
$$

These use a product of exponentials.

Euler angles are a special case of Lie-Cartan coordinates of the second kind.

For basis vectors representing rotations around the $z$, $y$, and $x$ axes:

$$\Large
w_1 =
\begin{pmatrix}
0\\0\\1
\end{pmatrix},
\qquad
w_2 =
\begin{pmatrix}
0\\1\\0
\end{pmatrix},
\qquad
w_3 =
\begin{pmatrix}
1\\0\\0
\end{pmatrix},
$$

the coordinates $\beta_1,\beta_2,\beta_3$ are Euler angles.

Intuition:

Lie-Cartan coordinates describe a curved object, the Lie group, by moving from the identity in directions given by the Lie algebra.

---

## Links

[[3D Computer Vision]]