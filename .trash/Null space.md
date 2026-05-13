# Definition
The nullspace of a matrix $A \in \mathbb{R}^{m \times n}$ is the set of all vectors mapped to zero by $A$.
$$\Large
\mathcal{N}(A) = \{x \in \mathbb{R}^n : Ax = 0\}
$$

---
## Dimension Context
- Vectors in $\mathcal{R}(A)$ live in $\mathbb{R}^m$
- Vectors in $\mathcal{N}(A)$ live in $\mathbb{R}^n$

## Orthogonal Complement Relationship

$$\Large
\mathcal{R}(A^T) = \mathcal{N}(A)^\perp
$$

Together:

$$\Large
\{w : w = u + v,\ u \in \mathcal{R}(A^T),\ v \in \mathcal{N}(A)\}
=
\mathbb{R}^n
$$

And:

$$\Large
\mathcal{R}(A^T) \cap \mathcal{N}(A) = \{0\}
$$

---
# Links
[[Linear Algebra]]
[[3D Computer Vision]]
