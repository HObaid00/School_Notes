# Rodrigues' Formula

Rodrigues' formula gives a closed-form expression for the matrix exponential of a skew-symmetric matrix.

For $\hat{w} \in \mathfrak{so}(3)$:

$$\Large
e^{\hat{w}}
=
I
+
\frac{\hat{w}}{|w|}
\sin(|w|)
+
\frac{\hat{w}^2}{|w|^2}
\left(
1-\cos(|w|)
\right)
$$

This formula is useful because it avoids computing the infinite matrix exponential series directly.

It is analogous to Euler's formula for complex numbers:

$$\Large
e^{i\phi}
=
\cos(\phi) + i\sin(\phi)
$$

The vector $w$ contains both the rotation axis and the rotation angle:

- the direction of $w$ is the rotation axis,
- the magnitude $|w|$ is the rotation angle.

Let:

$$\Large
t = |w|,
\qquad
v = \frac{w}{|w|}
$$

Then:

$$\Large
\hat{w} = \hat{v}t
$$

The powers of $\hat{v}$ simplify:

$$\Large
\hat{v}^2 = vv^\top - I,
\qquad
\hat{v}^3 = -\hat{v}
$$

Because of this repeating pattern, the exponential series separates into sine and cosine terms, producing Rodrigues' formula.

Intuition:

Rodrigues' formula turns an axis-angle vector into a rotation matrix.

---

## Links

[[3D Computer Vision]]