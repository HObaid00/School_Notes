# The Lie Bracket

The **Lie bracket** measures the non-commutativity of two elements in a Lie algebra.

For two skew-symmetric matrices $\hat{w}, \hat{v} \in \mathfrak{so}(3)$, the Lie bracket is:

$$\Large
[\hat{w}, \hat{v}]
=
\hat{w}\hat{v}
-
\hat{v}\hat{w}
$$

If the matrices commute, then:

$$
\hat{w}\hat{v}
=
\hat{v}\hat{w}
$$

and the Lie bracket is zero.

But rotations generally do **not** commute. Rotating around the $x$-axis and then the $y$-axis usually gives a different result from rotating around the $y$-axis and then the $x$-axis.

So the Lie bracket captures the difference between these two orders.

In $\mathfrak{so}(3)$, the Lie bracket is closely related to the cross product:

$$\Large
[\hat{w}, \hat{v}]
=
\widehat{w \times v}
$$

Intuition:

The Lie bracket tells us how much two infinitesimal rotations fail to commute.

---

## Links

[[3D Computer Vision]]