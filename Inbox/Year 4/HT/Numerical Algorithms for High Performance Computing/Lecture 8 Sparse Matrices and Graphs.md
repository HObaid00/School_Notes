Winter 2025/2026  

---

# 1. PageRank and Sparse Matrices

## Graph Model

- Websites → nodes  
- Hyperlinks → edges  
- Adjacency matrix:
  $$
  A_{ij} =
  \begin{cases}
  1 & \text{if link } i \to j \\
  0 & \text{otherwise}
  \end{cases}
  $$

---

## Random Surfer Model

Let:

- $x_i$ = fraction of surfers at page $i$
- $\sum_i x_i = 1$

Update rule:

$$
x_i^{(n+1)} = \sum_j \rho_j A_{ji} x_j^{(n)}
$$

where:

$$
\rho_j = \frac{1}{n_j}
$$

and

$$
n_j = \sum_l A_{jl}
$$

Define:

$$
B_{ij} = \frac{1}{n_j} (A^T)_{ij}
$$

Then:

$$
x^{(n+1)} = B x^{(n)}
$$

---

## PageRank with Damping

$$
x^{[m]} = \alpha B x^{[m-1]} + (1-\alpha)\frac{1}{n}e
$$

- Power iteration
- $B$ sparse → SpMV
- Cost per iteration: $\mathcal{O}(\text{nnz}(B))$

---

# 2. Sparse Matrices and Graphs

## Graph of a Matrix

Given $A \in \mathbb{R}^{n\times n}$:

- Vertices: $e_1, \dots, e_n$
- Edge $(e_i,e_k)$ iff $a_{ik} \ne 0$

Directed for general matrices  
Undirected if $A$ symmetric.

---

## Adjacency Matrix of Graph

$$
A(G(A))_{ij} =
\begin{cases}
1 & a_{ij} \ne 0 \\
0 & \text{otherwise}
\end{cases}
$$

---

## Symmetric Permutation

$$
\hat A = P A P^T
$$

Effect:

- Simultaneous row/column reordering
- Equivalent to renumbering vertices of graph

Graph structure unchanged, ordering changed.

---

# 3. Bandwidth Reduction

Bandwidth = max distance of nonzero from diagonal.

Goal: reduce bandwidth to:

- Improve locality
- Reduce fill-in in direct solvers

---

# 4. Cuthill–McKee Reordering

Goal: small bandwidth.

## Idea

Breadth-first search (BFS):

- Build level sets:
  $$
  S_1, S_2, S_3, \dots
  $$
- Order vertices by BFS traversal

Produces spanning tree ordering.

---

## Algorithm (Queue-Based)

```
Initialize P[1..n] = 0
active = {start node}
i = 1

while active not empty:
    v = pop(active)
    for all j with A[v,j] ≠ 0:
        if P[j] = 0:
            append(active,j)
            P[j] = i
            i = i + 1
```

Returns new numbering.

---

## Reverse Cuthill–McKee

Reverse ordering:

$$
i \mapsto n-i
$$

Often:

- Smaller fill-in
- Better practical results

---

# 5. Reordering to Reduce Fill-In

Block structure example:

Permute matrix into:

$$
\begin{pmatrix}
A_1 & 0 \\
0 & A_2
\end{pmatrix}
$$

Block diagonal form:

- Subsystems independent
- Easier inversion

---

# 6. Dissection Reordering

Matrix reordered into:

$$
\begin{pmatrix}
A_{11} & 0 & A_{13} \\
0 & A_{22} & A_{23} \\
A_{31} & A_{32} & A_{33}
\end{pmatrix}
$$

Separator block: $A_{33}$.

---

## LU Structure

$$
L_{33}U_{33}
=
A_{33}
-
\sum_i A_{3i} A_{ii}^{-1} A_{i3}
$$

→ Schur complement

---

# 7. Nested Dissection

Idea:

1. Cut graph by separator
2. Number separator last
3. Recurse

For 2D Poisson ($n\times n$ grid):

$$
\mathcal{O}(n^3)
$$

operations.

Goal:

- Small separator
- Minimal graph cut