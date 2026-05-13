# Range, Kernel, and Rank

## Range

The range of a matrix contains all vectors reachable by:

$$\Large y = Ax$$

Formally:

$$\Large \text{range}(A)=\{y\mid \exists x: Ax=y\}$$

The range equals the span of the matrix columns.

#### Equivalent Meaning
A vector $v$ is in the range of $A$ if it can be written as a linear combination of the columns of $A$.

#### Example
$$\Large
A = \begin{bmatrix} 1 & 2 \\ 3 & 6 \end{bmatrix}  
$$
  
$$\Large
Ax = x_1 \begin{bmatrix} 1 \\ 3 \end{bmatrix} + x_2 \begin{bmatrix} 2 \\ 6 \end{bmatrix}  
$$
  
Notice:  
$$\Large
\begin{bmatrix} 2 \\ 6 \end{bmatrix} = 2 \begin{bmatrix} 1 \\ 3 \end{bmatrix}  
$$
  
**Range:**  
$$\Large
\text{Range}(A) = \text{span} \left\{ \begin{bmatrix} 1 \\ 3 \end{bmatrix} \right\}  
$$

### Projection Onto Range
For full-rank $A$ with $n < m$:

$$\Large
\operatorname{Proj}(y; A)
=
A(A^T A)^{-1}A^T y
$$

#### Special Case: Projection Onto a Line

For $a \in \mathbb{R}^m$:

$$\Large
\operatorname{Proj}(y; a)
=
\frac{aa^T}{a^T a}y
$$

---

## Kernel (Null Space)

The kernel contains all vectors mapped to zero:

$$\Large \ker(A)=\{x\mid Ax=0\}$$

These vectors disappear under the transformation.

---

## Solving Linear Systems

The equation:

$$\Large Ax=b$$

has a solution only if:

$$\Large b \in \text{range}(A)$$

---

## Uniqueness

Solutions are unique only if:

$$\Large \ker(A)=\{0\}$$

Otherwise infinitely many solutions exist.

---

## Rank

The rank measures the dimension of the range:

$$\Large \text{rank}(A)=\dim(\text{range}(A))$$
or in equivalent terms number of independent columns
$$\Large
\text{rank}(A) = \text{\# of independent columns}
$$
---

## Rank-Nullity Theorem

One of the most important results:

$$\Large \text{rank}(A)+\dim(\ker(A))=n$$

where $n$ is the number of columns.

---

## Interpretation

- High rank → more information preserved
- Low rank → compression or degeneracy

---
## Properties
- $\text{rank}(A) \leq \min(m,n)$
- $\text{rank}(A) = \text{rank}(A^T)$
- $\text{rank}(AB) \leq \min(\text{rank}(A), \text{rank}(B))$

---
## Applications

Rank is central in:

- Data compression
- Least squares
- Machine learning
- Computer vision
- PCA

---
# Links
[[Linear Algebra]]
[[3D Computer Vision]]