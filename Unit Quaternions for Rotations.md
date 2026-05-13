# Unit Quaternions for Rotations

A **unit quaternion** is a quaternion with norm one:

$$\Large
|q|=1
$$

Equivalently:

$$\Large
w^2+x^2+y^2+z^2=1
$$

Unit quaternions are useful for modeling 3D rotations because they avoid singularities and gimbal lock.

They are also convenient for:

- composing rotations,
- interpolating rotations,
- representing smooth camera or object orientation.

To rotate a 3D vector using a unit quaternion, first embed the vector as a pure quaternion:

$$\Large
p = v_xi + v_yj + v_zk
$$

A pure quaternion has zero real part.

Then apply the sandwich product:

$$\Large
p' = qpq^*
$$

The result $p'$ is again a pure quaternion. Its imaginary components give the rotated 3D vector.

To rotate by angle $\theta$ around a unit axis $(u_x,u_y,u_z)$, choose:

$$\Large
q
=
\cos\left(\frac{\theta}{2}\right)
+
\sin\left(\frac{\theta}{2}\right)
(u_xi + u_yj + u_zk)
$$

This quaternion represents the rotation compactly and avoids Euler-angle gimbal lock.

Useful figure to insert:
- Slide 33 shows the unit quaternion constraint, the sandwich product $p'=qpq^*$, and the axis-angle quaternion formula.

---

## Links

[[3D Computer Vision]]