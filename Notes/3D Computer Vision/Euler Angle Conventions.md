# Euler Angle Conventions

Euler angles depend on the order in which rotations are applied.

A rotation can be represented as a product of three axis rotations:

$$\Large
R =
\exp(\beta_1\hat{w}_1)
\exp(\beta_2\hat{w}_2)
\exp(\beta_3\hat{w}_3)
$$

Each factor is a rotation around one coordinate axis.

For example:

$$\Large
R_x(\theta)
=
\begin{pmatrix}
1 & 0 & 0 \\
0 & \cos\theta & -\sin\theta \\
0 & \sin\theta & \cos\theta
\end{pmatrix}
$$

$$\Large
R_y(\theta)
=
\begin{pmatrix}
\cos\theta & 0 & \sin\theta \\
0 & 1 & 0 \\
-\sin\theta & 0 & \cos\theta
\end{pmatrix}
$$

$$\Large
R_z(\theta)
=
\begin{pmatrix}
\cos\theta & -\sin\theta & 0 \\
\sin\theta & \cos\theta & 0 \\
0 & 0 & 1
\end{pmatrix}
$$

Different fields use different conventions:

- Aerospace often uses ZYX, also called yaw-pitch-roll.
- Classical mechanics often uses ZXZ.
- Robotics often uses ZYZ.

The most important rule is:

$$\Large
\text{Always state the Euler angle convention explicitly.}
$$

Without specifying the convention, three angles are ambiguous.

Useful figure to insert:
- Slide 28 shows the standard rotation matrices $R_x$, $R_y$, and $R_z$, and emphasizes that the Euler angle convention must always be stated.

---

## Links

[[3D Computer Vision]]