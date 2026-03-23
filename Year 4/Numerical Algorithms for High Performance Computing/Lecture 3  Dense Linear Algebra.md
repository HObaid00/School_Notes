## Dwarf #1 - Dense Linear Algebra

Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# The Seven Dwarfs of HPC

1. Dense Linear Algebra  
2. Sparse Linear Algebra  
3. Spectral Methods  
4. N-body Methods  
5. Structured Grids  
6. Unstructured Grids  
7. Monte Carlo  

---

# Part I – Communication-Optimal Matrix Multiplication

Case study:  
Demmel et al., *Communication-Optimal Parallel Recursive Rectangular Matrix Multiplication*, IPDPS 2013.

---

## Background: Parallel Matrix Multiplication

### Cannon’s Algorithm

- Requires $p \times p$ processor grid  
- Uses rectangular blocks  
- Each processor stores three blocks  

Blocking strategies:

- **2D distribution** → split work in two dimensions  
- **3D distribution** → split work in three dimensions  
- **2.5D variants**  

---

## Breadth-First (BFS) vs Depth-First (DFS)

Split example:

$$
A(B_1\ B_2) = (C_1\ C_2)
$$

- **BFS**:
  - Compute $AB_1$ and $AB_2$ in parallel
  - Each uses $p/2$ processors
  - Replicates $A$

- **DFS**:
  - Compute sequentially
  - Uses all $p$ processors
  - More communication

Trade-off:

- BFS → less communication, more memory  
- DFS → less memory, more communication  

---

# CARMA Algorithm

Recursive strategy:

1. Split largest dimension
2. If enough memory → BFS
3. Else → DFS

Pseudo-structure:

```
if P = 1:
  SequentialMultiply
if enough memory:
  BFS recursion
else:
  DFS recursion
```

Properties:

- Communication-optimal
- Cache- and network-oblivious
- Adapts to memory

---

## Communication Model

- $P$ processors
- Local memory size $M$
- Count:
  - Words transferred (bandwidth)
  - Messages (latency)

Let:

$$
d_1 = \min(m,n,k), \quad
d_2 = \text{median}(m,n,k), \quad
d_3 = \max(m,n,k)
$$

---

## One Large Dimension

Example:

$$
n \gg k = m
$$

Communication (PEM model):

$$
p \cdot km + nk + nm
$$

Memory overhead:

$$
(p - 1) \cdot km
$$

---

## Two Large Dimensions

Example:

$$
m = k \gg n
$$

Recursive alternating split along $m$ and $k$.

Each processor loads:

- $A_{i,j}$
- $B_j$
- $C_i$

Communication cost:
(see tutorials)

---

## Three Large Dimensions

Ordered:

$$
d_3 \ge d_2 \ge d_1
$$

Phases:

1. Split along $d_3$
2. Alternate splits $d_3$, $d_2$
3. Round-robin splitting all 3 dimensions

Memory replication must be analysed.

---

# Part II – LU Decomposition

Goal:

Given matrix $A$, find:

$$
LU = A
$$

- $L$ lower triangular
- $U$ upper triangular

Solve:

$$
Ly = b, \quad Ux = y
$$

---

## Sequential LU (Right-Looking)

For $k = 1 \dots n-1$:

$$
l_{i,k} = \frac{a_{i,k}}{a_{k,k}}
$$

Update:

$$
a_{i,j} = a_{i,j} - l_{i,k} a_{k,j}
$$

Cost:

$$
mn^2 - \frac{n^3}{3}
$$

---

# Blocked LU

Partition:

$$
A =
\begin{pmatrix}
A_{11} & A_{12} \\
A_{21} & A_{22}
\end{pmatrix}
$$

Steps:

1. Factor $A_{11}$
2. Compute $L_{21}, U_{12}$
3. Update trailing matrix:

$$
A_{22} := A_{22} - L_{21}U_{12}
$$

Blocking improves:

- Cache efficiency
- Parallelism

---

# Tile-Oriented LU

Operate on tiles:

- Panel factorisation
- Panel updates
- Trailing matrix updates

Leads to many independent tile tasks:

$$
L_{j,k} U_{k,k} = A^*_{j,k}
$$

$$
A^*_{i,j} = A^*_{i,j} - L_{i,k} U_{k,j}
$$

---

# Parallel Matrix Distribution

## 1D Block Distribution

$$
\varphi(i,j) = \left\lfloor \frac{j p}{N} \right\rfloor
$$

Problem:
- Load imbalance

---

## Column Cyclic

$$
\varphi(i,j) = j \bmod p
$$

Better balance,
but cache inefficiency.

---

## 2D Block Cyclic (Standard)

$$
\varphi(i,j) =
\left(
\left\lfloor \frac{i}{b} \right\rfloor \bmod p_x,
\left\lfloor \frac{j}{b} \right\rfloor \bmod p_y
\right)
$$

Advantages:

- Good load balance
- Enables BLAS-3
- Used in ScaLAPACK

*(Copy 2D block-cyclic distribution diagram from slide 26.)*

---

# Graph-Oriented Parallelisation

Construct DAG:

- Nodes = tile operations
- Edges = dependencies

Data hazards:

- RAW (true dependency)
- WAR
- WAW

Use task-based scheduling.

---

# LU with Partial Pivoting (GEPP)

For each column $k$:

1. Find max in $A(k:m,k)$
2. Swap rows
3. Eliminate below pivot

Communication:

$$
O(n \log p_r)
$$

---

# Tournament Pivoting (TSLU)

Block-recursive pivot search.

Binary tree reduction:

- Each processor performs GEPP locally
- Combine results in $\log P$ steps

Communication-avoiding LU:

$$
O\left(\frac{n}{b} \log p_r\right)
$$

instead of

$$
O(n \log p_r)
$$

---

# CALU Complexity (Sketch)

For square matrix:

Computation:

$$
\gamma \cdot \left(
\frac{2n^3}{3p}
+ \text{lower-order terms}
\right)
$$

Communication:

$$
\beta \frac{n^2}{\sqrt{p}}
$$

Latency:

$$
\lambda \sqrt{p} \log^3 p
$$

---

# Libraries for Dense Linear Algebra

## BLAS

- Level 3: matrix multiplication
- Blocking for cache efficiency

## LAPACK

- Linear systems
- Eigenproblems

## PBLAS / ScaLAPACK

- Distributed memory
- 2D block-cyclic layout

---

# Modern Libraries

## PLASMA

- DAG-based scheduling
- Tile algorithms

## MAGMA

- GPU variant

## FLAME

- Formal algorithm derivation

---

# Programming Model Support

## OmpSs

- Task-based
- Dependency annotations

## OpenMP (≥ 4.0)

Example:

```
#pragma omp task depend(out:x)
#pragma omp task depend(in:x)
```

---

# Summary

Dense linear algebra in HPC requires:

- Communication-optimal algorithms (CARMA)
- Blocking and tiling
- 2D block-cyclic distribution
- Task-based parallelisation (DAG)
- Communication-avoiding pivoting (CALU)

Performance is dominated by:

- Communication volume
- Latency
- Memory hierarchy efficiency
- Load balance