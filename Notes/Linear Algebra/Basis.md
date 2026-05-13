# Basis

A set of vectors $B = \{v_1, \dots, v_n\}$ is called a **basis of** $V$ if it is linearly independent and if it spans the vector space $V$. A basis is maximal set of linearly independent vector.

---
# Properties

Let $B$ and $B'$ be two bases of a linear space $V$.
1. $B$ and $B'$ contain the same number of vectors. This number $n$ is called the **dimension of the space** $V$.
2. Any vector $v \in V$ can be uniquely expressed as a linear combination of the basis vectors in $B = \{b_1, \dots, b_n \}$: $$\Large v = \sum_{i=1}^n \alpha_i b_i$$
3. In particular, all vectors of $B$ can be expressed as linear combinations of vectos of anther basis $b' \in B$: $$\Large  
b_i' = \sum_{j=1}^n \alpha_{ji} b_j$$
4. The coefficients $\alpha_{ij}$ for this **basis transform** can be combined in a matrix A. Setting $B \equiv (b_1, \dots , b_n)$  and $B' \equiv (b_1', \dots, b_n')$ as the matrices of basis vectors, we can write: $$\Large  
B' = BA \quad \Leftrightarrow \quad B = B' A^{-1}  $$


# Links
[[Basis and Linear Independence]]
[[Linear Algebra]]
[[3D Computer Vision]]