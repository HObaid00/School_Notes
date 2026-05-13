# The Rotation Group $SO(3)$

The group $SO(3)$ is the set of all valid 3D rotation matrices.

It is defined as:

$$\Large
SO(3)
=
\{ R \in \mathbb{R}^{3 \times 3}
\mid
R^\top R = I,\ \det(R)=1
\}
$$

The condition

$$
R^\top R = I
$$

means that $R$ preserves lengths and angles. Such a matrix is called **orthogonal**.

The condition

$$
\det(R)=1
$$

means that the transformation preserves orientation. It excludes reflections, which have determinant $-1$.

The name $SO(3)$ means:

- $S$: special, meaning determinant $+1$,
- $O$: orthogonal,
- $3$: acting in three dimensions.

A rotation matrix acts on a 3D point or vector as:

$$\Large
X' = RX
$$

Example:

A rotation around the $z$-axis by an angle $\theta$ is:

$$\Large
R_z(\theta)
=
\begin{pmatrix}
\cos\theta & -\sin\theta & 0 \\
\sin\theta & \cos\theta & 0 \\
0 & 0 & 1
\end{pmatrix}
$$

The group property means that multiplying two rotation matrices gives another rotation matrix:

$$\Large
R_1, R_2 \in SO(3)
\Rightarrow
R_1R_2 \in SO(3)
$$

This is important because applying two rotations sequentially is still just one rotation.

---

## Links

[[3D Computer Vision]]