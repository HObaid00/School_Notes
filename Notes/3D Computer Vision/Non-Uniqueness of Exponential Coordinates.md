# Non-Uniqueness of Exponential Coordinates

For every rigid-body motion $g \in SE(3)$, there exists a twist $\hat{\xi} \in \mathfrak{se}(3)$ such that:

$$\Large
g = \exp(\hat{\xi})
$$

However, this representation is not unique.

The reason is similar to rotations in $SO(3)$. A rotation by angle $\theta$ is equivalent to a rotation by:

$$\Large
\theta + 2\pi k
$$

for any integer $k$.

Since $SE(3)$ contains $SO(3)$ as its rotational component, the same non-uniqueness appears for rigid-body transformations.

Given:

$$\Large
g =
\begin{pmatrix}
R & T \\
0 & 1
\end{pmatrix},
$$

we first find $w$ such that:

$$\Large
e^{\hat{w}} = R
$$

Then we solve for the linear velocity component $v$ such that the translational part matches $T$.

The key point is:

$$\Large
\text{many different twists can produce the same rigid-body motion}
$$

This matters in optimization because the same physical pose can have multiple coordinate descriptions.

----

## Links

[[Exponential Coordinates]]
[[3D Computer Vision]]