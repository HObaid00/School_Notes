# Euler Angles

Euler angles are a way to represent a 3D rotation using three angles.

Instead of representing a rotation by a full $3 \times 3$ matrix, Euler angles use a sequence of three rotations around coordinate axes.

A general idea is:

$$\Large
R =
\exp(\beta_1 \hat{w}_1)
\exp(\beta_2 \hat{w}_2)
\exp(\beta_3 \hat{w}_3)
$$

Here:

- $\hat{w}_1, \hat{w}_2, \hat{w}_3$ are basis elements of $\mathfrak{so}(3)$,
- $\beta_1, \beta_2, \beta_3$ are the Euler angles.

For example, if the axes are chosen as $z$, $y$, and $x$, then the three angles may correspond to yaw, pitch, and roll.

Euler angles are examples of **Lie-Cartan coordinates of the second kind**, because they are built as a product of exponentials.

Important warning:

Euler angles are only a **local parameterization** of $SO(3)$. They cannot represent all rotations globally without singularities.

Intuition:

Euler angles are easy to understand because they describe rotation as “turn around this axis, then this axis, then this axis.” But their simplicity comes with problems such as convention ambiguity and gimbal lock.

---

## Links

[[3D Computer Vision]]
