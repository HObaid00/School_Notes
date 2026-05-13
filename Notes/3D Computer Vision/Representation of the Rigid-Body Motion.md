# Representation of Rigid-Body Motion

A rigid-body motion in 3D can be represented using:

1. a rotation matrix $R \in \mathbb{R}^{3 \times 3}$,
2. a translation vector $T \in \mathbb{R}^3$.

The transformation of a point $x$ is:

$$\Large
g_t(x) = Rx + T
$$

The rotation matrix describes how the coordinate axes rotate. If the original basis vectors are $e_1, e_2, e_3$, then their transformed versions are:

$$
r_i = g_t(e_i)
$$

The vectors $r_1, r_2, r_3$ form the columns of $R$:

$$\Large
R =
\begin{pmatrix}
| & | & | \\
r_1 & r_2 & r_3 \\
| & | & |
\end{pmatrix}
$$

Because rigid-body motion preserves lengths and angles, the columns of $R$ must be orthonormal:

$$\Large
R^\top R = I
$$

Because the motion also preserves orientation, we require:

$$\Large
\det(R) = +1
$$

The set of all valid 3D rotation matrices is called the **special orthogonal group**:

$$\Large
SO(3)
=
\{ R \in \mathbb{R}^{3 \times 3}
\mid
R^\top R = I,\ \det(R)=1
\}
$$

So a rigid-body motion is described by:

$$\Large
x \mapsto Rx + T
$$

where $R \in SO(3)$ and $T \in \mathbb{R}^3$.

---

## Links

[[3D Computer Vision]]