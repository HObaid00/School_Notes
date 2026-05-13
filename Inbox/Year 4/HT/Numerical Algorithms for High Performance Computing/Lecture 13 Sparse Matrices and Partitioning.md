# Numerical Algorithms for HPC  
## Sparse Matrices and Partitioning  

Michael Bader  
TUM – SCCS  
Winter 2024/2025  

---

# Part I: Parallel SpMV & Graph Partitioning

---

# Sparse Matrix–Vector Multiplication

We consider sparse matrix–vector multiplication

$$
y = Ax
$$

with vectors $y, x \in \mathbb{R}^n$ and sparse matrix  
$A \in \mathbb{R}^{n \times n}$.

We require:

- A mapping of each non-zero element $a_{ij} \ne 0$ to a partition:

$$
a_{ij} \rightarrow P(\varphi(i,j)), \quad 1 \le i,j \le n
$$

- A mapping of each vector element:

$$
y_i \rightarrow P(\varphi_v(i)), \qquad
x_j \rightarrow P(\varphi_v(j))
$$

We use the same distribution $\varphi_v$ for both vectors $x$ and $y$.

---

# Parallel SpMV – Communication Phases

Main phases:

1. **Fanout**  
   Get elements $x_j$ for which $\varphi(j) = p$.

2. **Local computation**  
   For rows $i$ mapped to processor $p$:
   $$
   \sum_j a_{ij} x_j
   $$

3. **Fanin**  
   Collect contributions to $y_i$ from other processors.

4. **Final sum**  
   Accumulate contributions to obtain $y_i$.

---

# SpMV in the BSP Model

Supersteps:

- compute #1: –
- communicate #1: fanout
- synchronize #1

- compute #2: local computation
- communicate #2: fanin
- synchronize #2

- compute #3: sum up contributions
- communicate #3: –
- synchronize #3

For successive SpMVs, supersteps #3 and #1 can be merged.

---

# SpMV and Graph Partitioning

## Minimize Communication

From sparse matrix $A$, construct graph $(V,E)$:

- Each row/column becomes a vertex:
  $$
  V = \{1,\dots,n\}
  $$

- Each nonzero defines an edge:
  $$
  (i,j) \in E \iff a_{ij} \ne 0
  $$

(assumes $n \times n$ symmetric adjacency graph)

Perform multilevel $k$-partitioning:

- Balanced partitions
- Minimize edge cut

---

# SpMV and Edge Cut Minimization

Result:

- Partition rows $\{1,\dots,n\}$ to processors $\{1,\dots,p\}$.
- Use as distribution $\varphi_v$ for $x$ and $y$.
- Row-wise matrix partitioning:
  $$
  \varphi(i,j) := \varphi_v(i)
  $$

### Communication Consequences

- All nonzeros of row $i$ stored with $y_i$.
  → No fanin required.

- A cut edge means:
  - $a_{ij}$ and $x_j$ are on different processors.
  - Each cut edge causes transfer of $x_j$.

---

# Example: SpMV on an Unstructured Grid

Assumptions:

- Unknowns located on mesh vertices.
- $a_{ij} \ne 0$ iff vertices $i,j$ share a mesh edge.

![[Pasted image 20260303122601.png]]

---

# Edge Cut vs Communication

Minimizing edge cut ≠ minimizing communication.

Reasons:

- Several cut edges may require only one transfer of $x_j$.
- No 1:1 relation between edge cut and communication volume.

### Work Balance

- Graph partitioning balances rows.
- Work depends on number of nonzeros per row.

Remedy:

- Weighted graph.
- Use number of nonzeros per row as vertex weights.

---

# Part II  
## Mondriaan Partitioning

![[Pasted image 20260303122623.png]]

---

# Recall: Cartesian Matrix Partitioning

Example:

- $59 \times 59$ matrix
- 312 nonzeros
- $p = 4$

Nonzeros per processor:

```
126, 28, 128, 30
```

Each separate split is optimally balanced (for blocks).

![[Pasted image 20260303122645.png]]

---

# Non-Cartesian Matrix Partitioning

Same matrix:

- 312 nonzeros
- $p = 4$

Nonzeros per processor:

```
76, 76, 80, 80
```

Balanced per processor.

![[Pasted image 20260303122705.png]]

---

# $p$-Way Matrix Partitioning

Define:

$$
A_s = \{(i,j) : 0 \le i,j < n \land \varphi(i,j)=s\}
$$

Interpretation:

- Nonzero ≡ index pair.
- Sparse matrix ≡ set of index pairs.

Partition:

$$
A = \{(i,j) : a_{ij} \ne 0\}
$$

$$
A_0,\dots,A_{p-1}
$$

forms a $p$-way partition.

Notation:

$$
V(A_0,\dots,A_{p-1}) = V_\varphi
$$

---

# Communication Volume

For partition:

$$
V(A_0,A_1,A_2,A_3)
$$

Decomposition:

$$
V(A_0,A_1,A_2,A_3)
=
V(A_0,A_1,A_2 \cup A_3)
+
V(A_2,A_3)
$$

Interpretation:

- Total communication volume equals volume of coarse split plus local split.

![[Pasted image 20260303122731.png]]

---

# Motivation of Mondriaan Splitting

## Theorem (without proof)

Given $m \times n$ sparse matrix $A$ and disjoint subsets:

$$
A_0,\dots,A_k
$$

then:

$$
V(A_0,\dots,A_k)
=
V(A_0,\dots,A_{k-2}, A_{k-1} \cup A_k)
+
V(A_{k-1},A_k)
$$

### Meaning

- Step from $k$ to $k+1$ parts done locally.
- Only one split needs to be considered.
- Greedy minimization of communication.

---

## Mondriaan Partitioning

- Recursive bisection of matrix.
- Rows and columns need not be consecutive.
- Minimizes communication volume directly.

---

# Example: Matrix `prime60`

- $60 \times 60$
- 462 nonzeros
- $p=4$
- Imbalance tolerance $\varepsilon = 3\%$

Results:

- Max nonzeros per processor: 117
- Average: $462/4 = 115.5$
- Achieved imbalance: $\approx 1.3\%$

Communication:

- fanout: 51
- fanin: 47
- total:
  $$
  V = 98
  $$

![[Pasted image 20260303122755.png]]

---

# Local View of `prime60`

Local submatrix sizes:

- $29 \times 26$ for $P(0)$
- $29 \times 34$ for $P(1)$
- $31 \times 31$ for $P(2)$
- $31 \times 29$ for $P(3)$

![[Pasted image 20260303122807.png]]

---

# Hypergraph Partitioning

## Column Bipartitioning

Hypergraph:

$$
H = (V,N)
$$

- Columns ≡ vertices
- Rows ≡ hyperedges (nets)

Net definition:

$$
n_i = \{ j : a_{ij} \ne 0 \}
$$

Cut hyperedges correspond exactly to communication.

![[Pasted image 20260303122829.png]]

---

## Row Bipartitioning

- Rows ≡ vertices
- Columns ≡ hyperedges

Net:

$$
n_j = \{ i : a_{ij} \ne 0 \}
$$

Balanced partitions:

- Assign full rows or columns.
- Vertex weight = number of nonzeros.
- Weighted partitioning balances work.

Copy picture from **Slide 19**.

---

# Reference

Rob H. Bisseling:

*Parallel Scientific Computing –  
A structured approach using BSP and MPI.*  
Oxford University Press, 2004.