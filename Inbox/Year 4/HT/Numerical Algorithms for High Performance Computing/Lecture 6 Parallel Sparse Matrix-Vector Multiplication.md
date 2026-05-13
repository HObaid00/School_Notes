(Original slides by Rob Bisseling, Universiteit Utrecht)  
Winter 2025/2026  

---

# 1. Building a Distributed Sparse Matrix

Two approaches:

1. Start with a global sparse matrix → then distribute elements.
2. **Distribute first** → then build local sparse data structures.

Preferred: **distribute first (a-priori distribution)**

- Assign index subsets of potential nonzeros to processors.
- Subsets form a partition of the nonzero set:
  - disjoint
  - cover all nonzeros
- Use standard sequential sparse formats locally.
- Avoid communication for insert/delete.

---

# 2. General Matrix Distribution

Most general scheme:

$$
a_{ij} \mapsto P(\phi(i,j)),
\quad 0 \le i,j < n, \; a_{ij} \ne 0
$$

where:

$$
0 \le \phi(i,j) < p
$$

- Zeros are not assigned.
- Define $\phi(i,j) = -1$ if $a_{ij}=0$.
- 1D processor numbering assumed.
- Sparsity pattern known a priori.

---

# 3. SpMV: Where to Compute $a_{ij} v_j$?

Sparse matrix-vector multiplication:

$$
u_i = \sum_j a_{ij} v_j
$$

Observation:

$$
\text{nz}(A) \gg n
$$

→ Move vector components $v_j$ to nonzeros $a_{ij}$.

Key idea:

1. Move required $v_j$.
2. Compute local products $a_{ij} v_j$.
3. Accumulate local partial sums:
   $$
   u_i^{(s)}
   $$
4. Send partial sums to owner of $u_i$.
5. Final accumulation.

Only communicate:

- vector components $v_j$
- partial sums $u_i^{(s)}$

Never communicate matrix entries.

---

# 4. Vector Distribution

Map vector components:

$$
u_i \mapsto P(\phi_u(i)),
\quad 0 \le i < n
$$

Usually:

$$
\text{distr}(u) = \text{distr}(v)
$$

Exception:

For $A^T A v$:
- distribution may change between operations.

---

# 5. Local Computation

Local partial sum on processor $P(s)$:

$$
u_i^{(s)}
=
\sum_{0 \le j < n, \; \phi(i,j)=s}
a_{ij} v_j
$$

Exploit sparsity:

- Only nonzeros are processed.
- Only locally nonempty rows are considered.

---

# 6. Row Index Set

Define locally nonempty rows:

$$
I_s =
\{ i :
0 \le i < n \land
\exists j \text{ with } \phi(i,j)=s \}
$$

Example:

- $I_0 = \{0,1,2,3\}$
- $I_1 = \{0,2,3,4\}$

Rows without local nonzeros are ignored.

---

# 7. Local SpMV

For all $i \in I_s$:

$$
u_i^{(s)} := 0
$$

For all $j$ with $\phi(i,j)=s$:

$$
u_i^{(s)} := u_i^{(s)} + a_{ij} v_j
$$

---

# 8. Local Sparse Data Structure

Use adapted CRS:

- Only store nonempty local rows.
- Reindex rows locally:
  $$
  i = \text{rowindex}[i]
  $$
- `start[i]` marks first local nonzero.

---

# 9. Column Index Set

Define locally nonempty columns:

$$
J_s =
\{ j :
0 \le j < n \land
\exists i \text{ with } \phi(i,j)=s \}
$$

Example:

- $J_0 = \{0,1,2\}$
- $J_1 = \{2,3,4\}$

---

# 10. Superstep (0): Fanout

For all $j \in J_s$:

$$
\text{get } v_j
\text{ from } P(\phi_v(j))
$$

Important:

- Receiver knows it needs $v_j$.
- Sender does not.
- Requires explicit **get** primitive.

Contrast:
- Dense algorithms → predictable communication.

---

# 11. Superstep (1): Local Multiply

$$
u_i^{(s)}
=
\sum_{\phi(i,j)=s}
a_{ij} v_j
$$

Cost:

$$
T(1) = \frac{2 c n}{p} + l
$$

where:

- $c$ = average nonzeros per row
- $l$ = latency

---

# 12. Superstep (2): Fanin

For all $i \in I_s$:

$$
\text{put } u_i^{(s)}
\text{ in } P(\phi_u(i))
$$

---

# 13. Superstep (3): Final Summation

For local $u_i$:

$$
u_i = \sum_{t=0}^{p-1} u_i^{(t)}
$$

Cost:

$$
T(3) = n + l
$$

---

# 14. Cost Analysis (BSP Model)

Assume:

- Nonzeros evenly distributed:
  $$
  \frac{cn}{p}
  $$
  per processor
- Vector evenly distributed:
  $$
  \frac{n}{p}
  $$

---

## Fanout Cost

Receive:

$$
h_{recv} = n - \frac{n}{p}
$$

Send:

$$
h_{send} = \frac{n}{p}(p-1)
$$

Cost:

$$
T(0) =
\left(1 - \frac{1}{p}\right) ng + l
$$

---

## Fanin Cost

Same as fanout:

$$
T(2) =
\left(1 - \frac{1}{p}\right) ng + l
$$

---

# 15. Total BSP Cost

$$
T_{MV}
\le
\frac{2cn}{p}
+
n
+
2\left(1-\frac{1}{p}\right)ng
+
4l
$$

BSP weights normalized:

- $g = \beta/\gamma$
- $l = \lambda/\gamma$

---

# 16. Efficiency Condition

Computation efficient if:

$$
\frac{2cn}{p} > 2ng
$$

i.e.

$$
c > pg
$$

Rarely satisfied except for very dense matrices.

---

## Improving Efficiency

- Use Cartesian (2D) distribution.
- Automatic structure detection.
- Exploit matrix classes:
  - random sparse
  - Laplacian matrices

---

# 17. Communication Volume

Let:

- $p_i$ = processors having nonzeros in row $i$
- $q_j$ = processors having nonzeros in column $j$

Lower bound:

$$
V_\phi
=
\sum_{i: p_i \ge 1} (p_i - 1)
+
\sum_{j: q_j \ge 1} (q_j - 1)
$$

Upper bound:

$$
V_\phi + 2n
$$

---

# 18. Summary

- **Distribute first, represent later.**
- General mappings:
  $$
  a_{ij} \mapsto P(\phi(i,j))
  $$
  $$
  u_i \mapsto P(\phi_u(i))
  $$
- 4 supersteps:
  1. Fanout
  2. Local multiply
  3. Fanin
  4. Summation
- Row set $I_s$ and column set $J_s$ exploit sparsity.
- Essential use of **get** primitive.

