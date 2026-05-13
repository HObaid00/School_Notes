# Hyperplanes and Decision Boundaries

Linear classifiers separate classes using hyperplanes.

---

# Hyperplane Equation

A hyperplane is defined by:

$$\Large
w^Tx+w_0=0
$$

where:

- $w$ = normal vector
- $w_0$ = bias term

---

# Interpretation

For any point $x$:

$$
w^Tx+w_0
\begin{cases}
>0 & \text{one side}\\
=0 & \text{on the plane}\\
<0 & \text{other side}
\end{cases}
$$

---

# Geometry

The vector $w$ is perpendicular to the hyperplane.

It determines the orientation of the decision boundary.

![[Pasted image 20260227105524.png]]

---

# Linear Separability

A dataset is linearly separable if there exists a hyperplane perfectly separating the classes.

---

# Example

In 2D:

$$\Large
w_1x_1+w_2x_2+w_0=0
$$

defines a line.

In 3D:

$$
w_1x_1+w_2x_2+w_3x_3+w_0=0
$$

defines a plane.

In higher dimensions, it becomes a hyperplane.

---
# Links
[[Machine Learning]]