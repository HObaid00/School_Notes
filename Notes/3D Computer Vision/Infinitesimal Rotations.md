# Infinitesimal Rotations

An infinitesimal rotation is a very small rotation. Instead of studying one fixed rotation matrix, we consider a smooth path of rotations $R(t)$.

Assume:

$$\Large
R(t) \in SO(3)
$$

and

$$\Large
R(0) = I
$$

A point moves according to:

$$\Large
X_{\text{trans}}(t) = R(t)X_{\text{orig}}
$$

Since $R(t)$ is always a rotation matrix, it satisfies:

$$\Large
R(t)R(t)^\top = I
$$

Differentiate this equation:

$$\Large
\frac{d}{dt}(RR^\top)
=
\dot{R}R^\top + R\dot{R}^\top = 0
$$

This implies:

$$\Large
\dot{R}R^\top
=
-(\dot{R}R^\top)^\top
$$

So $\dot{R}R^\top$ is skew-symmetric.

Because every $3 \times 3$ skew-symmetric matrix corresponds to some vector $w \in \mathbb{R}^3$, we can write:

$$\Large
\dot{R}(t)R(t)^\top = \hat{w}(t)
$$

Equivalently:

$$\Large
\dot{R}(t) = \hat{w}(t)R(t)
$$

At $t=0$, where $R(0)=I$:

$$\Large
\dot{R}(0) = \hat{w}(0)
$$

Therefore, a tiny rotation can be approximated by:

$$\Large
R(dt) \approx I + \hat{w}(0)dt
$$

This shows that skew-symmetric matrices describe infinitesimal rotations.

---

## Links

[[3D Computer Vision]]