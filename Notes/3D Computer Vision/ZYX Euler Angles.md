# ZYX Euler Angles

The ZYX convention applies rotations in the order:

$$\Large
R(\psi,\theta,\phi)
=
R_z(\psi)R_y(\theta)R_x(\phi)
$$

Here:

- $\psi$ is yaw, rotation around the $z$-axis,
- $\theta$ is pitch, rotation around the $y$-axis,
- $\phi$ is roll, rotation around the $x$-axis.

The resulting rotation matrix is:

$$\Large
R(\psi,\theta,\phi)
=
\begin{pmatrix}
\cos\psi\cos\theta &
\cos\psi\sin\theta\sin\phi - \sin\psi\cos\phi &
\cos\psi\sin\theta\cos\phi + \sin\psi\sin\phi
\\
\sin\psi\cos\theta &
\sin\psi\sin\theta\sin\phi + \cos\psi\cos\phi &
\sin\psi\sin\theta\cos\phi - \cos\psi\sin\phi
\\
-\sin\theta &
\cos\theta\sin\phi &
\cos\theta\cos\phi
\end{pmatrix}
$$

This representation uses only three numbers, which seems convenient. However, it has singular configurations.

The problematic case occurs when:

$$\Large
\theta = \frac{\pi}{2}
$$

At this value, the matrix loses one independent degree of freedom. This is the beginning of the gimbal lock problem.

Useful figure to insert:
- Slide 29 shows the full ZYX Euler angle rotation matrix and the special case when $\theta=\frac{\pi}{2

---

## Links

[[3D Computer Vision]]