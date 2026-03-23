Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# On the Model of Computation

Classical asymptotic complexity ($O(n)$, $O(n^2)$, …) is often insufficient in HPC.

Performance depends on multiple aspects:

- Data access
- Computation
- Communication
- Scalability / parallelism

Conclusion:
We need **multiple performance models** to analyse different bottlenecks.

---

# Part I — PRAM (Parallel Random Access Machine)

## PRAM Model

- Shared global memory
- Arbitrarily many processors $P_1, \dots, P_n$
- Central control (SIMD / lockstep execution)

### Access Variants

- **EREW** — Exclusive Read, Exclusive Write  
- **CREW** — Concurrent Read, Exclusive Write  
- **ERCW**
- **CRCW**

If multiple processors write different values concurrently → undefined result.

*(Copy Exclusive/Concurrent read/write diagrams from slide 5.)*

---

## Lockstep Execution

Parallel loops execute synchronously.

Example:

```
for i from 1 to n do in parallel {
  if U[i] > 0
    F[i] = (U[i] - U[i-1]) / dx
  else
    F[i] = (U[i+1] - U[i]) / dx
}
```

Execution order:

1. All processors evaluate condition simultaneously.
2. All "then" branches execute.
3. All "else" branches execute.

Substeps are synchronised → no concurrent read within a substep.

---

## Example: Minimum Search

Binary fan-in reduction.

Algorithm (EREW PRAM):

```
for i from 0 to k−1 do
  for j from 1 to n by 2^(i+1) do in parallel
    if L[j+2^i] < L[j]
      L[j] := L[j+2^i]
return L[1]
```

Complexity:

$$
T(n) = \Theta(\log n)
$$

on $\frac{n}{2}$ processors.

---

## PRAM vs MPI Collectives

Comparable operations:

- MPI Reduce
- MPI Bcast
- MPI Gather / AllGather
- MPI Scatter
- MPI AllToAll
- MPI Barrier

Typical complexity:
- Logarithmic (tree-based)

---

## PRAM Matrix Multiplication (CREW)

```
for i = 1..n in parallel
  for k = 1..n in parallel
    for j = 1..n
      C[i,k] += A[i,j] * B[j,k]
```

- $n^2$ processors
- Runtime: $O(n)$
- Concurrent reads of A and B

---

## Forcing EREW Access (Shifted Indices)

$$
C[i,k] +=
A[i,(i+j+k) \bmod n]
\cdot
B[(i+j+k) \bmod n,k]
$$

Ensures exclusive read access.

---

# Part II — Parallel External Memory (PEM)

## Memory Model

- External shared memory
- Each CPU has private cache of size $M$
- Cache line size $L$
- Complexity measured in cache line transfers

![[Pasted image 20260301192330.png]]

---

## Example: 1D Stencil

```
for i = 1..n
  xnew[i] = 0.25 * (x[i-1] + 2x[i] + x[i+1])
```

Memory behaviour:

- Access: $x[i-1], x[i], x[i+1], xnew[i]$
- Cache line transfer every $L$ iterations

Total transfers:

$$
2 \left\lceil \frac{n}{L} \right\rceil
$$

---

## Cache Approaches

### 1. I/O Model (“Out-of-Core”)

- Explicit control of memory transfers

### 2. Cache-Oblivious

- Intelligent eviction
- Algorithm independent of $M$ and $L$

Memory complexity:
- Count cache line transfers
- Basis for Roofline analysis

---

# Roofline Model and Cache

- Roofline counts main memory accesses
- Requires cache model to estimate actual traffic
- Stride access reduces effective bandwidth
- Improved locality → higher arithmetic intensity

![[Pasted image 20260301192221.png]]

---

# Matrix Multiplication — Naive (PEM)

Each processor:

- Reads $2n$ elements
- Performs $2n$ flops

Arithmetic intensity:

$$
1 \text{ flop per word}
$$

→ memory-bound.

---

# Blocked Matrix Multiplication (PEM)

Block size $b$ such that:

$$
3b^2 \le M
$$

Memory transfers per processor:

- C block: $2b^2$
- A and B blocks: $\frac{2n}{b} b^2$

Total transfers (all processors):

$$
\Theta\left(\frac{n^3}{L\sqrt{M}}\right)
$$

Arithmetic intensity:

$$
\Theta(b)
$$

→ compute-bound if $b$ sufficiently large.

---

# Block-Recursive Multiplication

- Recursive divide-by-2 strategy
- Automatically adapts to cache hierarchy

![[Pasted image 20260301210732.png]]

---

# Part III — BSP (Bulk Synchronous Parallelism)

## BSP Model

- Processors with private memory
- Point-to-point network
- Computation organised in **super steps**

Each super step:

1. Local computation
2. Communication
3. Barrier synchronisation

---

## BSP Cost Model

Parameters:

- $\gamma$ — time per operation
- $\beta$ — time per byte transferred
- $\lambda$ — latency

For $s$ super steps:

$$
T = s(n\gamma + m\beta + \lambda)
$$

---

## BSP Example: Minimum Search

### Super Step 1

- Local comparisons: $n/p$
- Root receives $p$ words

$$
T_1 = \frac{n}{p}\gamma + 4p\beta + \lambda
$$

### Super Step 2

- Root computes min of $p$ elements

$$
T_2 = p\gamma + \lambda
$$

---

# BSP Intricacies

Computation:

$$
n = \max_i n_i
$$

Communication:

$$
m = \max_i m_i
$$

Overlap of communication & computation:
- Not considered in pure BSP

Collective operations:
- Must be analysed separately

---

# Matrix Multiplication — BSP

2D processor grid ($p \times p$).

Each processor holds one block:

Block size:

$$
\frac{n}{p} \times \frac{n}{p}
$$

---

## BSP Time Complexity

Computation per super step:

$$
T_{comp} = \gamma (n/p)^3
$$

Communication per super step:

$$
T_{comm} = 2\beta n^2/p
$$

Latency:

$$
T_{lat} = \lambda
$$

Total (≈ $p$ steps):

$$
T_{BSP}(n,p)
=
\gamma \frac{n^3}{p^2}
+
2\beta n^2
+
\lambda p
$$

---

# Cannon’s Algorithm (BSP)

Each super step:

- Multiply local blocks
- Cyclically shift A and B blocks

Communication per step:

$$
2\beta (n/p)^2
$$

Total runtime:

$$
T_{BSP}(n,p)
=
\gamma \frac{n^3}{p^2}
+
2\beta \frac{n^2}{p}
+
\lambda p
$$

---

# Summary — Parallel Models

Each model captures a different bottleneck:

- **PRAM** → theoretical parallel limits
- **Parallel External Memory** → cache effects
- **Roofline** → memory vs compute bound
- **BSP** → computation vs communication trade-off

No single model suffices.

Select the model matching the dominant bottleneck.