# Lie Groups and Lie Algebras

A **Lie group** is a mathematical object that is both:

1. a group,
2. a smooth manifold.

This means we can multiply elements, invert them, and also do calculus on them.

The rotation group $SO(3)$ is a Lie group because:

- rotations can be multiplied,
- every rotation has an inverse,
- rotations vary smoothly with their parameters.

The corresponding **Lie algebra** is the tangent space at the identity element of the Lie group.

For $SO(3)$, the Lie algebra is:

$$\Large
\mathfrak{so}(3)
=
\{ \hat{w} \mid w \in \mathbb{R}^3 \}
$$

That is, $\mathfrak{so}(3)$ is the space of all $3 \times 3$ skew-symmetric matrices.

Intuition:

- The Lie group $SO(3)$ contains finite rotations.
- The Lie algebra $\mathfrak{so}(3)$ contains infinitesimal rotations.

The Lie algebra lets us describe small motions linearly, even though rotations themselves live on a curved space.

Useful figure to insert:
- Slide 15 contains a helpful schematic showing the Lie group as a curved manifold and the Lie algebra as a tangent space. It also shows the exponential map from algebra to group and the logarithm map from group to algebra.

---

## Links

[[Matrix Groups]]
[[3D Computer Vision]]