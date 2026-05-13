## Definition
The range of a matrix $A \in \mathbb{R}^{m \times n}$ is the span of its columns.

$$\Large
\mathcal{R}(A) = \{v \in \mathbb{R}^m : v = Ax,\ x \in \mathbb{R}^n\}
$$

## Equivalent Meaning
A vector $v$ is in the range of $A$ if it can be written as a linear combination of the columns of $A$.

---
## Example
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

## Projection Onto Range

For full-rank $A$ with $n < m$:

$$\Large
\operatorname{Proj}(y; A)
=
A(A^T A)^{-1}A^T y
$$

## Special Case: Projection Onto a Line

For $a \in \mathbb{R}^m$:

$$\Large
\operatorname{Proj}(y; a)
=
\frac{aa^T}{a^T a}y
$$

---
# Links
[[Linear Algebra]]
