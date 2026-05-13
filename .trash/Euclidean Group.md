## Definition
A Euclidean transformation $L$ from $\mathbb R^n$ to $\mathbb R^n$ is defined by an orthogonal matrix $R \in O(n)$ and a vector $T \in \mathbb R^n$:
$$\Large
L: \mathbb R^n \to \mathbb R^n; \quad x \to L = Rx + T
$$
The set of all such transformations is called the **Euclidean group** $E(n)$. It is a subgroup of the affine group $A(n)$. Embedded by homogeneous coordinates, we get:  

$$\Large
E(n) = \{
\begin{pmatrix}  
R & T \\  
0 & 1  
\end{pmatrix}
\mid  R \in O(n), T \in \mathbb R^n
\}
$$
If $R \in SO(n)$ (i.e. $det(R)= 1$), then we have the **special Euclidean group** $SE(n)$. In particular, $SE(3)$ represents the **rigid-body motions** in $\mathbb R^3$.

---
## Summery
$$\Large
SO(n) \subset O(n) \subset GL(n), \quad SE(n) \subset E(n) \subset A(n) \subset (GL+1)
$$
Where $x \subset y$ means x is a subset of y.

---
## Links
[[3D Computer Vision]]