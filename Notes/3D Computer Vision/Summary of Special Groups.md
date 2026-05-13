# Summary of $SO(3)$ and $SE(3)$

The group $SO(3)$ represents pure 3D rotations.

The group $SE(3)$ represents full 3D rigid-body motions, combining rotation and translation.

## Rotation: $SO(3)$

A rotation matrix satisfies:

$$\Large
R^\top R = I,
\qquad
\det(R)=1
$$

It acts on a point or vector as:

$$\Large
X = RX_0
$$

The inverse is:

$$\Large
R^{-1}=R^\top
$$

The exponential representation is:

$$\Large
R = \exp(\hat{w})
$$

The velocity equation is:

$$\Large
\dot{X} = \hat{w}X
$$

The adjoint action is:

$$\Large
\hat{w} \mapsto R\hat{w}R^\top
$$

## Rigid-body motion: $SE(3)$

A rigid-body transformation is:

$$\Large
g =
\begin{pmatrix}
R & T \\
0 & 1
\end{pmatrix}
$$

It acts on a point as:

$$\Large
X = RX_0 + T
$$

The inverse is:

$$\Large
g^{-1}
=
\begin{pmatrix}
R^\top & -R^\top T \\
0 & 1
\end{pmatrix}
$$

The exponential representation is:

$$\Large
g = \exp(\hat{\xi})
$$

The velocity equation is:

$$\Large
\dot{X} = \hat{w}X + v
$$

The adjoint action is:

$$\Large
\hat{\xi} \mapsto g\hat{\xi}g^{-1}
$$

Useful figure to insert:
- Slide 26 contains a summary table comparing $SO(3)$ and $SE(3)$, including matrix representation, coordinate action, inverse, exponential representation, velocity, and adjoint map.

---
