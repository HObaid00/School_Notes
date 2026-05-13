# Matrix Multiplication

$$\Large
C = AB, \quad C_{ij} = \sum_{k=1}^{n} A_{ik} B_{kj}
$$

## Conditions
- $A \in \mathbb{R}^{m \times n}$
- $B \in \mathbb{R}^{n \times p}$

## Views

### 1. Row × Column
$$\Large
C_{ij} = a_i^T b_j
$$

### 2. Column Combination
$$\Large
Ax = \sum_{i=1}^n x_i a_i
$$

### 3. Outer Product Form
$$\Large
AB = \sum_{i=1}^n a_i b_i^T
$$

## Properties
- Associative: $(AB)C = A(BC)$
- Distributive: $A(B + C) = AB + AC$
- Not commutative: $AB \neq BA$

---
# Links
[[Linear Algebra]]
