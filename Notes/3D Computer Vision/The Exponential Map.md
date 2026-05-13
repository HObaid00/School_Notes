# The Exponential Map for $SO(3)$

The **exponential map** converts an infinitesimal rotation from the Lie algebra $\mathfrak{so}(3)$ into a finite rotation in the Lie group $SO(3)$.

Suppose $\hat{w}$ is constant in time and the rotation matrix satisfies:

$$\Large
\dot{R}(t) = \hat{w}R(t),
\qquad
R(0)=I
$$

The solution is:

$$\Large
R(t)
=
e^{\hat{w}t}
$$

The matrix exponential is defined by the infinite series:

$$\Large
e^{\hat{w}t}
=
\sum_{n=0}^{\infty}
\frac{(\hat{w}t)^n}{n!}
=
I + \hat{w}t + \frac{(\hat{w}t)^2}{2!} + \cdots
$$

If $\|w\|=1$, then $e^{\hat{w}t}$ is a rotation around the axis $w$ by angle $t$.

More generally, the exponential map is:

$$\Large
\exp : \mathfrak{so}(3) \rightarrow SO(3),
\qquad
\hat{w} \mapsto e^{\hat{w}}
$$

Intuition:

The Lie algebra stores a rotation as an axis and magnitude. The exponential map turns that compact infinitesimal description into an actual rotation matrix.

---

## Links

[[3D Computer Vision]]