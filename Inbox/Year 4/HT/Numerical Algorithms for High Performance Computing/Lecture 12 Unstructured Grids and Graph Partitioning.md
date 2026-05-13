# Numerical Algorithms for HPC  
## Dwarf #6 – Unstructured Grids and Graph Partitioning  

Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# Parallelization of Unstructured-Grid Computations

## Load Distribution and Communication

- Divide grid into partitions (e.g. one per CPU/core).
- Uniform computational load  
  → partitions of equal size.
- Minimal communication effort  
  → minimise number of grid cells at partition boundaries.

![[Pasted image 20260303121254.png]]

---

## BSP Super-Step

Typical super-step in BSP model:

1. Perform partition-local update (access replicated ghost-cell data).
2. Exchange data to update ghost cells  
   → send cell-local data for each boundary cell.
3. Synchronise.

### Main Influences on Parallel Execution Time

- Equal load balance  
  → minimise size of largest partition.
- Minimise number of boundary cells.

![[Pasted image 20260303121254.png]]

---

# Partitioning Unstructured Grids

## Problem Setting

Divide grid into $K$ partitions:

- Equal number of grid cells  
  (or equal collective weight).
- Minimal number of cells at the boundary.

Objective:
- Count (weighted?) boundary edges (or vertices).

![[Pasted image 20260303121355.png]]

---

# Graph-Based Partitioning

## Graph Representation of Grids

### Standard Graph $(V,E)$

- $V$ = grid vertices  
- $E$ = grid cell edges  

### Dual Graph $(V',E')$

- $V'$ = grid cells  
- $E'$ = adjacency of grid cells  

![[Pasted image 20260303121428.png]]

---

# $K$-Way Graph Partitioning

Divide $V$ (or $V'$) into $K$ partitions $V_k$:

$$
V_k \cap V_j = \emptyset \quad (k \ne j)
$$

$$
\bigcup_k V_k = V
$$

Balance constraint:

$$
|V_k| = \frac{|V|}{K} \pm \varepsilon_k
$$

### Objective: Minimise Edge Cut

Edge cut:

$$
\{(e,f) \in E : e \in V_k,\ f \notin V_k\}
$$

- NP-complete problem  
- Use heuristic algorithms

![[Pasted image 20260303121444.png]]

---

# Multilevel $k$-Way Partitioning (MLkP)

Algorithm (Karypis & Kumar, 1998):

### 1. Coarsening Phase

- Collapse sets of vertices.
- Preserve vertex and edge weights.

### 2. Partitioning Phase

- Perform $K$-way partitioning on coarse graph.

### 3. Uncoarsening Phase

- Expand collapsed vertices.
- Apply local refinement after each expansion.

---

# Coarsening Phase

## Matching

Matching = set of independent edges  
(no two edges share a vertex).

Maximal matching:
- No further edges can be added.
- Some vertices may remain unmatched.

Perfect matching:
- Covers all vertices.

### Matching-Based Coarsening

If $(u,v)$ is matched  
→ collapse into single coarse vertex.

---

## Collapse Graph After Matching

### Coarse Vertices

Given matching $M_i$ on $(V_i,E_i)$:

- Each $m \in M_i$ becomes vertex $v_m$ in $V_{i+1}$.
- Each unmatched vertex remains.
- Vertex weight:

$$
W(v_m) = W(u) + W(v)
$$

### Coarse Edges

Edge between two coarse vertices if an edge existed between their fine members.

Edge weights summed over such connections.

Stop if:
- Graph small enough.
- Matching no longer sufficiently reduces size.

---

# Algorithms for Matching

## Random Matching

- Visit vertices in random order.
- Unmatched vertex $u$ selects random unmatched neighbour $v$.
- Add $(u,v)$ to matching.

Greedy, simple, does not optimise edge cut.

---

## Heavy Edge Matching (HEM)

Use edge weights $W(e)$.

For set of edges $A$:

$$
W(A) = \sum_{e \in A} W(e)
$$

After matching $M_i$:

$$
W(E_{i+1}) = W(E_i) - W(M_i)
$$

Heuristic:

- Prefer edges with large weight.
- Greedy selection of heaviest adjacent unmatched edge.

Goal: keep edge cut small.

---

## Modified Heavy Edge Matching

Idea: coarse graphs with low average degree give better partitions.

For vertex $v$:

- Determine $H(v)$ = edges to unmatched neighbours with largest weight.

Define:

$$
W_c(v,u) = \sum W(e)
$$

over edges:
- $e = (u,u')$
- where $u'$ is also connected to $v$

Choose $(v,u)$ maximising $W_c(v,u)$.

---

# Partitioning the Coarse Graph

Options:

- Coarsen until $k$ vertices remain  
  → often bad balance.
- Recursive bisection (recommended).
- Spectral partitioning (Fiedler vector).
- Geometric methods.
- Combinatorial methods.

---

# Uncoarsening Phase

## Backprojection

If coarse vertex $m = (u,v)$ is in partition $p$  
→ assign $u$ and $v$ to $p$ in fine graph.

---

## Local Refinement

Greedy improvement:

- Swap vertices between partitions.
- Reduce edge cut.
- Maintain load balance.

---

# Local Refinement Algorithm

For vertex $v$:

1. Determine neighbouring partitions $N(v)$.
2. For each $B \in N(v)$ compute gain:

$$
g(v,B)
$$

3. Move $v$ to $B$ if:
   - Gain largest and $> 0$
   - Balance constraints satisfied:

$$
W(B) + W(v) \le W_{\max}
$$

$$
W(A) - W(v) \ge W_{\min}
$$

Or if:
- $g(v,B)=0$ and balance improves.

---

## Gain Computation

External degree:

$$
ED(v,B) = \sum_{u \in P_B} W(v,u)
$$

Internal degree:

$$
ID(v) = \sum_{u \in P_A} W(v,u)
$$

Gain:

$$
g(v,B) = ED(v,B) - ID(v)
$$

---

# MLkP Example – Coarsening Phase

Start with dual graph.

![[Pasted image 20260303121541.png]]

---

## Random Matching

Copy picture from **Slides 20–25**.

![[Pasted image 20260303121616.png]]
![[Pasted image 20260303121633.png]]
![[Pasted image 20260303121648.png]]


Collapsing leads to weighted vertices.

---

# MLkP Example – Partitioning

Initial partition on coarse graph:

- Example values:
  - edge-cut: 11
  - balance: 25–26–19

![[Pasted image 20260303121712.png]]

---

# MLkP Example – Uncoarsening

Inflate collapsed vertices.

Apply local refinement.

Examples:

- edge-cut: 11 → balance improved.
- Later:
  - edge-cut: 11
  - balance: 24–24–22

Copy pictures from **Slides 29–32**.

![[Pasted image 20260303121746.png]]

Final result (random matching):

- edge-cut: 11
- balance: 24–24–22

---

# Comparison with Better Partition

Example optimal(?):

- edge-cut: 9
- balance: 24–23–23

![[Pasted image 20260303121801.png]]

---

# Heavy Edge Matching Example

After heavy-edge matching:

Initial coarse partition:

- edge-cut: 14
- balance: 21–23–26

After refinement:

- edge-cut: 12
- balance: 25–19–26

Further refinement:

- edge-cut: 10
- balance: 23–22–25

Final:

- edge-cut: 9
- balance: 23–23–24

![[Pasted image 20260303121824.png]]

---

# Final Partition

Heavy-edge matching result:

- edge-cut: 9
- balance: 23–23–24

Very similar to best partition.

![[Pasted image 20260303121842.png]]

---

# References

- Karypis & Kumar (1998),  
  *A Fast and High Quality Multilevel Scheme for Partitioning Irregular Graphs*,  
  SIAM J. Sci. Comput.
- Karypis & Kumar (1998),  
  *Multilevel k-way Partitioning Scheme for Irregular Graphs*,  
  JPDC.
- Hendrickson & Leland (1995),  
  *A Multi-Level Algorithm for Partitioning Graphs*, SC’95.