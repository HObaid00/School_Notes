# Rigid-Body Motion

A **rigid-body motion** is a transformation that moves an object without changing its shape.

This means distances, angles, and orientation are preserved. If two points are fixed on the object, their distance stays the same after the motion.

A rigid-body motion $g_t$ maps points in $\mathbb{R}^3$ to new points:

$$\Large
g_t : \mathbb{R}^3 \rightarrow \mathbb{R}^3
$$

For vectors, a rigid-body motion preserves the norm:

$$\Large
|g_t(v)| = |v|
$$

It also preserves the cross product:

$$\Large
g_t(u) \times g_t(v) = g_t(u \times v)
$$

Because the norm and inner product are related by the polarization identity,

$$\Large
\langle u, v \rangle
=
\frac{1}{4}
\left(
|u+v|^2 - |u-v|^2
\right),
$$

a rigid-body motion also preserves inner products.

Rigid-body motions preserve volume because they preserve the triple product:

$$\Large
\langle g_t(u), g_t(v) \times g_t(w) \rangle
=
\langle u, v \times w \rangle
$$

Intuition:

A rigid-body motion can rotate and translate an object, but it cannot stretch, shear, or reflect it.

---
## Links

[[3D Computer Vision]]