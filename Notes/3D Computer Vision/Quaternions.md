# Quaternions

Quaternions extend complex numbers by adding two more imaginary units.

A quaternion has the form:

$$\Large
q = w + xi + yj + zk
$$

where:

$$
w,x,y,z \in \mathbb{R}
$$

The set of quaternions is:

$$\Large
\mathbb{H}
=
\{q = w + xi + yj + zk \mid w,x,y,z \in \mathbb{R}\}
$$

Here:

- $w$ is the real component,
- $x,y,z$ are imaginary components.

The defining relations are:

$$\Large
i^2 = j^2 = k^2 = ijk = -1
$$

Quaternion addition is component-wise.

Quaternion multiplication is:

- associative,
- not commutative.

That means:

$$\Large
q_1q_2 \neq q_2q_1
$$

in general.

This non-commutativity is useful for representing rotations, because 3D rotations themselves are also non-commutative.

---

## Links

[[3D Computer Vision]]