
(Original slides by Rob Bisseling, Universiteit Utrecht)  
Winter 2025/2026  

---

# 1. 1D vs 2D Processor Numbering

Use a 2D processor grid:

$$
P(s,t), \quad 0 \le s < M,\; 0 \le t < N
$$

Total processors:

$$
p = MN
$$

Column-wise identification:

$$
P(s,t) \equiv P(s + tM)
$$

Equivalent 1D ↔ 2D mapping:

$$
P(s) \equiv P(s \bmod M,\, s \div M)
$$

---

# 2. Cartesian Matrix Distribution

A Cartesian distribution $(\phi_0, \phi_1)$ maps:

$$
\phi(i,j) = (\phi_0(i), \phi_1(j))
$$

or in 1D numbering:

$$
\phi(i,j) = \phi_0(i) + \phi_1(j) M
$$

Thus:

- Processor row determined by $\phi_0(i)$
- Processor column determined by $\phi_1(j)$

---

# 3. Advantages of Cartesian Distribution

### Advantages

- Row-wise operations require communication **only within processor rows**.
- Column-wise operations require communication **only within processor columns**.
- Each $v_j$ sent to at most $M$ processors.
- Each $u_i$ collects contributions from at most $N$ processors.
- Rectangular submatrix partitioning (clean structure).

### Disadvantage

- Less general than arbitrary nonzero mappings.
- May not yield globally optimal distribution.

---

# 4. Matching Matrix and Vector Distribution

Observation:

Processors holding nonzeros $a_{ij}$ lie in processor column:

$$
P(\ast, \phi_1(j))
$$

Assign:

- $v_j$ to a processor in $P(\ast, \phi_1(j))$
- $u_i$ to a processor in $P(\phi_0(i), \ast)$

Effects:

- $v_j$ sent to at most $M-1$ processors.
- $u_i$ receives from at most $N-1$ processors.
- Communication reduced.

---

# 5. Theorem 4.4 (Key Property)

Let:

1. $A$ be distributed Cartesian: $(\phi_0, \phi_1)$.
2. $u_i$ stored in $P(\phi_0(i), \ast)$.
3. $v_j$ stored in $P(\ast, \phi_1(j))$.

Then:

If $u_i$ and $v_j$ reside on the same processor, then $a_{ij}$ is also local.

### Proof Sketch

If:

$$
u_i \in P(\phi_0(i), t)
$$
$$
v_j \in P(s, \phi_1(j))
$$

and both are the same processor, then:

$$
(s,t) = (\phi_0(i), \phi_1(j))
$$

Hence that processor owns $a_{ij}$.

---

# 6. Special Case: distr(u) = distr(v)

If:

- Matrix distribution is Cartesian.
- $u$ and $v$ distributed identically.

Then:

$$
u_i, v_i \in P(\phi_0(i), \phi_1(i))
$$

which is the processor owning diagonal element $a_{ii}$.

Thus:

- Matrix distribution determines vector distribution.
- And vice versa.

---

# 7. Example: 1D Laplacian Matrix

Tridiagonal matrix:

$$
A =
\begin{pmatrix}
-2 & 1 \\
1 & -2 & 1 \\
& 1 & -2 & 1 \\
& & \ddots & \ddots & \ddots \\
& & & 1 & -2 & 1 \\
& & & & 1 & -2
\end{pmatrix}
$$

Nonzeros:

$$
a_{ij} \ne 0 \iff i-j = 0, \pm 1
$$

---

# 8. Vector Distribution for Tridiagonal Case

Assume:

$$
\text{distr}(u) = \text{distr}(v)
$$

Theorem 4.4 implies:

Best to assign $u_i$, $v_i$, and neighbors $v_{i\pm1}$ to same processor.

Suitable distribution: **block distribution**

$$
u_i \mapsto P\!\left(\left\lfloor \frac{i}{\lceil n/p \rceil} \right\rfloor\right)
$$

This keeps neighboring indices local.

---

# 9. Cost Analysis (Cartesian Distribution)

Assume:

- Even nonzero distribution.
- Even vector distribution.
- Rows spread across processor rows.
- Columns spread across processor columns.

Superstep costs:

$$
T(0) = (M-1)\frac{n}{p} g + l
$$

$$
T(1) = \frac{2cn}{p} + l
$$

$$
T(2) = (N-1)\frac{n}{p} g + l
$$

$$
T(3) = \frac{Nn}{p} + l = \frac{n}{M} + l
$$

---

## Total Cost

$$
T_{MV,M\times N}
\le
\frac{2cn}{p}
+
\frac{n}{M}
+
\frac{M+N-2}{p} ng
+
4l
$$

---

# 10. Square Case: $M = N = \sqrt{p}$

Then:

$$
T_{MV,\sqrt{p}\times\sqrt{p}}
\le
\frac{2cn}{p}
+
\frac{n}{\sqrt{p}}
+
2\left(
\frac{1}{\sqrt{p}} - \frac{1}{p}
\right) ng
+
4l
$$

Efficiency condition:

$$
\frac{2cn}{p} >
\frac{2ng}{\sqrt{p}}
$$

i.e.

$$
c > \sqrt{p}\, g
$$

Improvement factor:

$$
\sqrt{p}
$$

compared to general 1D distribution.

---

# 11. Dense Matrix Case

Dense matrix = limit case:

$$
c \to n
$$

Cost becomes:

$$
T_{MV,dense}
\le
\frac{2n^2}{p}
+
\frac{n}{\sqrt{p}}
+
2\left(
\frac{1}{\sqrt{p}} - \frac{1}{p}
\right) ng
+
4l
$$

---

# 12. Block/Square Cyclic Distribution? No!

In square cyclic distribution:

- Diagonal element $a_{ii}$ assigned to:

$$
P(i \bmod \sqrt{p}, i \bmod \sqrt{p})
$$

Only $\sqrt{p}$ diagonal processors store diagonal.

Consequences:

- Vectors reside only on $\sqrt{p}$ processors.
- These processors must send many vector copies.

Cost:

$$
T_{MV,dense,\sqrt{p}\times\sqrt{p}\; cyclic}
=
\frac{2n^2}{p}
+
n
+
2\left(1 - \frac{1}{\sqrt{p}}\right) ng
+
4l
$$

Not optimal for SpMV.

---

# 13. Cyclic Row Distribution? No!

Choose:

$$
\phi_0(i) = i \bmod p
$$
$$
\phi_1(j) = 0
$$

Equivalent to:

$$
M=p, \quad N=1
$$

Cost:

$$
T_{MV,dense,p\times 1}
=
\frac{2n^2}{p}
+
\left(1-\frac{1}{p}\right) ng
+
2l
$$

Advantages:

- Skips fanin and final summation.
- Each row local.

Disadvantage:

- Very expensive fanout.
- Each processor sends $\frac{n}{p}$ components to all others.

---

# 14. Square Cartesian Distribution? Yes!

Procedure:

1. Use cyclic diagonal distribution:
   $$
   \phi_u(i) = \phi_v(i) = i \bmod p
   $$
2. Translate to 2D grid with:
   $$
   M = N = \sqrt{p}
   $$

Result:

- Balanced communication.
- Achieves optimal BSP cost.

---

# 15. Summary

- Use both 1D and 2D numbering:
  $$
  P(s,t) \equiv P(s + tM)
  $$
- Cartesian distributions restrict communication to processor rows/columns.
- For band matrices (e.g., tridiagonal), block vector distribution is effective.
- Square Cartesian distribution based on cyclic diagonal distribution:
  - Optimal for dense matrices.
  - Good for relatively dense sparse matrices.
- Other optimal distributions exist (e.g., block diagonal-based).