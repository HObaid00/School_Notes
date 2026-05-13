# Three-Dimensional Euclidean Space

Three-dimensional Euclidean space is the mathematical model of ordinary 3D space. It is denoted by $\mathbb{E}^3$.

A point in 3D space can be represented by coordinates:

$$\Large
X =
\begin{pmatrix}
X_1 \\
X_2 \\
X_3
\end{pmatrix}
\in \mathbb{R}^3
$$

Although $\mathbb{E}^3$ technically refers to points and $\mathbb{R}^3$ refers to coordinate vectors, in practice we often identify them and treat them similarly.

Given two points $X$ and $Y$, the vector from $Y$ to $X$ is:

$$\Large
v = X - Y
$$

This is called a **bound vector** if it is attached to a specific starting point. If we ignore its starting point and only care about its direction and length, it becomes a **free vector**.

Euclidean space allows us to define geometric quantities such as:

- distance,
- angles,
- curve length,
- area,
- volume.

For a curve $\gamma : [0,1] \rightarrow \mathbb{R}^3$, its length is:

$$\Large
l(\gamma) =
\int_0^1 |\dot{\gamma}(s)| \, ds
$$

Here, $\dot{\gamma}(s)$ is the velocity of the curve at parameter value $s$, and $|\dot{\gamma}(s)|$ is its speed.

Intuition:

If $\gamma(s)$ describes the position of a moving point, then the curve length is found by adding up all tiny distances traveled along the path.

---

## Links

[[3D Computer Vision]]