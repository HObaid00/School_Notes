# Moore–Penrose Pseudo inverse

The **Moore–Penrose pseudo inverse** is a generalization of the matrix inverse that applies to **non-square** or **singular matrices**. It is commonly denoted as:

$$\Large
A^\dagger
$$

for a given matrix \( A \).

---

## Definition

For a matrix $A \in \mathbb{R}^{m \times n}$, its pseudo-inverse $A^\dagger \in \mathbb{R}^{n \times m}$ is the unique matrix satisfying the following four **Penrose conditions**:

1. $A A^\dagger A = A$
2. $A^\dagger A A^\dagger = A^\dagger$
3. $(A A^\dagger)^T = A A^\dagger$
4. $(A^\dagger A)^T = A^\dagger A$

These ensure consistency, symmetry, and minimality properties.

---

## Intuition

- If $A$ is **square and invertible**, then:
  $$\Large
  A^\dagger = A^{-1}
  $$
- If $A$ is **not invertible or not square**, $A^\dagger$ provides the “best possible inverse.”

---

## Key Uses

### 1. Solving Linear Systems
For \( Ax = b \), when no exact solution exists:
$$\Large
x = A^\dagger b
$$
gives the **least-squares solution** (minimizes $|Ax - b\|$).

---

### 2. Minimum Norm Solution
Among all solutions to $Ax = b$, $A^+ b$ has the **smallest Euclidean norm**.

---

### 3. Data Science / ML
Used in:
- Linear regression (normal equation form)
- Dimensionality reduction
- Signal processing

---

## Computation via SVD

The most stable way to compute \( A^+ \) is using **Singular Value Decomposition (SVD)**:

$$\Large
A = U \Sigma V^T
$$

Then:

$$\Large
A^\dagger = V \Sigma^\dagger U^T
$$

Where:
- $\Sigma^\dagger$ is formed by taking the reciprocal of non-zero singular values
- Transposing the matrix

---

## Special Cases

### Full Column Rank (\( m > n \))

$$\Large
A^\dagger = (A^T A)^{-1} A^T
$$

### Full Row Rank (\( m < n \))
$$\Large
A^\dagger = A^T (A A^T)^{-1}
$$

---

## Geometric Interpretation

- $A^\dagger b$  is the projection of $b$ onto the **column space of $A$**
- Produces the closest achievable vector $Ax$ to $b$

---

## Summary

| Property | Description |
|--------|------------|
| Generalization | Works for any matrix |
| Unique | Only one pseudoinverse exists |
| Stable | Best computed via SVD |
| Practical | Used in least-squares and ML |

---

## Example (Conceptual)

If:
$$\Large
A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 6 \end{bmatrix}
$$

Then $A^\dagger$ is a $2 \times 3$ matrix that acts like an inverse in least-squares sense.

---

## Implementation (Python / NumPy)

```python
import numpy as np

A = np.array([[1, 2], [3, 4], [5, 6]])
A_pinv = np.linalg.pinv(A)

print(A_pinv)
```

---
# Moore-Penrose Pseudoinverse for SVD

## Motivation

Not all matrices are invertible.

- Some are rectangular
- Some are singular

The pseudoinverse generalizes matrix inversion.

---

## Definition

If:

$$\Large A = U\Sigma V^T$$

then the pseudoinverse is:

$$\Large A^\dagger = V\Sigma^\dagger U^T$$

where:

$$\Large \Sigma^\dagger$$

contains reciprocals of nonzero singular values.

---

## Solving Linear Systems

For:

$$\Large Ax=b$$

one solution is:

$$\Large x=A^\dagger b$$

---

## Least-Squares Interpretation

The pseudoinverse finds:

1. The least-squares solution
2. The minimum-norm solution

This is extremely important when systems are overdetermined.

---

## Applications

The pseudoinverse is used in:

- Linear regression
- Optimization
- Robotics
- Signal processing
- Neural networks
- Computer vision

---
# Links
[[3D Computer Vision]]