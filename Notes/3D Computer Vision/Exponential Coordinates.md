# Exponential Coordinates for $SE(3)$

The exponential map for $SE(3)$ converts a twist into a finite rigid-body motion.

Assume the twist $\hat{\xi}$ is constant and the transformation satisfies:

$$\Large
\dot{g}(t) = \hat{\xi}g(t),
\qquad
g(0)=I
$$

The solution is:

$$\Large
g(t) = e^{\hat{\xi}t}
$$

Using the matrix exponential:

$$\Large
e^{\hat{\xi}t}
=
\sum_{n=0}^{\infty}
\frac{(\hat{\xi}t)^n}{n!}
$$

For $t=1$, this gives a rigid-body transformation:

$$\Large
g = e^{\hat{\xi}}
$$

The exponential map is:

$$\Large
\exp : \mathfrak{se}(3) \rightarrow SE(3),
\qquad
\hat{\xi} \mapsto e^{\hat{\xi}}
$$

If $w=0$, meaning there is no rotation, the motion is pure translation:

$$\Large
e^{\hat{\xi}}
=
\begin{pmatrix}
I & v \\
0 & 1
\end{pmatrix}
$$

If $w \neq 0$, then the motion combines rotation and translation:

$$\Large
e^{\hat{\xi}}
=
\begin{pmatrix}
e^{\hat{w}} &
\frac{(I-e^{\hat{w}})\hat{w}v + ww^\top v}{|w|^2}
\\
0 & 1
\end{pmatrix}
$$

Intuition:

A twist tells us the instantaneous screw-like motion of a rigid body. The exponential map integrates this infinitesimal motion into a finite transformation.

---

## Links

[[3D Computer Vision]]
