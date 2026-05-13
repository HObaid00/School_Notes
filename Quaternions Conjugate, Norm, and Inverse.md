# Quaternion Conjugate, Norm, and Inverse

For a quaternion:

$$\Large
q = w + xi + yj + zk
$$

the conjugate is:

$$\Large
q^*
=
w - xi - yj - zk
$$

The norm is:

$$\Large
|q|^2
=
qq^*
=
w^2 + x^2 + y^2 + z^2
$$

The inverse is:

$$\Large
q^{-1}
=
\frac{q^*}{|q|^2}
$$

These are similar to complex numbers.

For a complex number:

$$
z = a + bi
$$

the conjugate is:

$$
z^* = a - bi
$$

and the squared norm is:

$$
|z|^2 = zz^* = a^2+b^2
$$

Quaternions generalize this idea to four components.

These operations are important for rotations because unit quaternions have:

$$\Large
|q|=1
$$

For a unit quaternion, the inverse simplifies to:

$$\Large
q^{-1}=q^*
$$

This makes rotation computations efficient.