# Representing Camera Motion

In 3D computer vision, the camera is often modeled as a moving coordinate frame.

Let the world frame be fixed and let the camera frame move over time. The motion from the world frame to the camera frame is represented by:

$$\Large
g(t)
=
\begin{pmatrix}
R(t) & T(t) \\
0 & 1
\end{pmatrix}
\in SE(3)
$$

At time $t=0$, the camera frame is assumed to coincide with the world frame:

$$\Large
g(0)=I
$$

For a world point $X_0$, its coordinates in the camera frame at time $t$ are:

$$\Large
X(t) = R(t)X_0 + T(t)
$$

In homogeneous coordinates:

$$\Large
X(t) = g(t)X_0
$$

This equation means that the same physical point has different coordinate values depending on the camera pose.

Intuition:

The point in the world may be stationary, but if the camera moves, the point appears to move in the camera coordinate system.

---

## Links

[[3D Computer Vision]]