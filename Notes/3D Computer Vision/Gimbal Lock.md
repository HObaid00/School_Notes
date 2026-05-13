# Gimbal Lock

**Gimbal lock** occurs when an Euler angle representation loses one degree of freedom.

For ZYX Euler angles:

$$\Large
R(\psi,\theta,\phi)
=
R_z(\psi)R_y(\theta)R_x(\phi)
$$

the singular case happens when:

$$\Large
\theta = \frac{\pi}{2}
$$

At this value, the rotation matrix depends only on the difference:

$$\Large
\psi - \phi
$$

Instead of depending independently on both $\psi$ and $\phi$.

The simplified form is:

$$\Large
R\left(\psi,\frac{\pi}{2},\phi\right)
=
\begin{pmatrix}
0 & -\sin(\psi-\phi) & \cos(\psi-\phi) \\
0 & \cos(\psi-\phi) & \sin(\psi-\phi) \\
-1 & 0 & 0
\end{pmatrix}
$$

This means that different triples of Euler angles can produce the exact same rotation matrix.

For example, all of the following have the same value of $\psi-\phi=30^\circ$:

| $\phi$ | $\theta$ | $\psi$ | $\psi-\phi$ |
|---:|---:|---:|---:|
| $30^\circ$ | $90^\circ$ | $60^\circ$ | $30^\circ$ |
| $50^\circ$ | $90^\circ$ | $80^\circ$ | $30^\circ$ |
| $0^\circ$ | $90^\circ$ | $30^\circ$ | $30^\circ$ |

Geometrically, after the $R_y(\frac{\pi}{2})$ rotation, two rotation axes become aligned in such a way that two rotations act in the same plane. Therefore, one independent rotation direction is lost.

Useful figure to insert:
- Slide 30 shows the gimbal lock simplification and a table of different Euler angle triples that produce the same rotation.

---

## Links

[[3D Computer Vision]]
