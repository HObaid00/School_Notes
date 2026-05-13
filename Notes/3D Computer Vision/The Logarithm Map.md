# The Logarithm Map for $SO(3)$

The **logarithm map** is the inverse of the exponential map. It converts a rotation matrix back into an element of the Lie algebra.

For a rotation matrix $R \in SO(3)$, there exists a vector $w \in \mathbb{R}^3$ such that:

$$\Large
R = \exp(\hat{w})
$$

The corresponding Lie algebra element is written as:

$$\Large
\hat{w} = \log(R)
$$

If $R \neq I$, the rotation angle is:

$$\Large
|w|
=
\cos^{-1}
\left(
\frac{\operatorname{trace}(R)-1}{2}
\right)
$$

The rotation axis is:

$$\Large
\frac{w}{|w|}
=
\frac{1}{2\sin(|w|)}
\begin{pmatrix}
r_{32} - r_{23} \\
r_{13} - r_{31} \\
r_{21} - r_{12}
\end{pmatrix}
$$

where $r_{ij}$ are the entries of $R$.

If $R=I$, then the rotation angle is zero:

$$\Large
|w| = 0
$$

Important note:

The representation is not unique. Rotating by an angle $\theta$ and by $\theta + 2\pi k$ around the same axis gives the same rotation matrix.

Intuition:

The logarithm map answers the question:

> “Given this rotation matrix, what axis-angle rotation produced it?”

---

## Links

[[3D Computer Vision]]