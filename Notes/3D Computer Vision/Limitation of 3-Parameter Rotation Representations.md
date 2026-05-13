# Limitations of 3-Parameter Rotation Representations

Euler angles are not the only rotation representation with singularities. Any global representation of $SO(3)$ using only three parameters must have singularities or discontinuities.

This is a topological issue: the space of 3D rotations cannot be covered smoothly by one global 3-coordinate chart.

In practice, this means:

- small changes in orientation can cause large changes in the parameters,
- interpolation can become unstable,
- optimization can behave poorly near singularities,
- animation may produce unexpected spinning or awkward motion.

Euler angles make this problem visible through gimbal lock, but the issue is more general.

The key idea is:

$$\Large
\text{No single smooth global 3-parameter representation can cover all of } SO(3)
$$

To avoid this, many systems use **unit quaternions**, which represent rotation using four numbers with one constraint.

Quaternions avoid gimbal lock because they use one extra parameter.

---

## Links

[[Quaternions]]
[[3D Computer Vision]]
