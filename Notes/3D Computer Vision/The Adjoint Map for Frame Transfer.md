# The Adjoint Map for Frame Transfer

The **adjoint map** describes how a twist changes when we express it in a different coordinate frame.

Suppose another frame is related to the current frame by a transformation $g_{xy}$:

$$\Large
Y = g_{xy}X(t)
$$

If the velocity in the original frame is represented by the twist $\hat{V}$, then the velocity in the new frame is:

$$\Large
\dot{Y}(t)
=
g_{xy}\dot{X}(t)
$$

Since:

$$\Large
\dot{X}(t) = \hat{V}X(t),
$$

we get:

$$\Large
\dot{Y}(t)
=
g_{xy}\hat{V}X(t)
$$

Using $X(t)=g_{xy}^{-1}Y(t)$:

$$\Large
\dot{Y}(t)
=
g_{xy}\hat{V}g_{xy}^{-1}Y(t)
$$

Therefore the transformed twist is:

$$\Large
\hat{V}_y
=
g_{xy}\hat{V}g_{xy}^{-1}
$$

This defines the adjoint map:

$$\Large
\operatorname{Ad}_g :
\mathfrak{se}(3) \rightarrow \mathfrak{se}(3),
\qquad
\hat{\xi}
\mapsto
g\hat{\xi}g^{-1}
$$

Intuition:

The same physical motion can have different coordinate values depending on the frame in which it is measured. The adjoint map converts twist coordinates between frames.

---

## Links

[[3D Computer Vision]]