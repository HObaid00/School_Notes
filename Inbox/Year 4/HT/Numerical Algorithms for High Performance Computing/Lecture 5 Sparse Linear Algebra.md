## Dwarf #2 – Sparse Linear Algebra  

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

# Part I – Data Structures for Sparse Matrices

A matrix is called **sparse** if it contains sufficiently many zero elements (i.e., sufficiently few non-zeros) such that it becomes worthwhile to use special data structures and algorithms to store and process it (Wilkinson).

---

# Coordinate Scheme (COO, Triple Scheme)

Store one triple $(a_{ij}, i, j)$ for each non-zero element.

### Storage Variants

**Array of Struct (AoS):**

```c
struct sparseElement {
    int i;
    int j;
    float a;
};
typedef struct sparseElement sparseMatrix[];
```

**Struct of Arrays (SoA):**

- Array `a[k]` → non-zero values  
- Array `i[k]` → row indices  
- Array `j[k]` → column indices  

Used e.g. in MATLAB or as input format.

---

## Example Matrix

Given triples:

```
a: 2, -1, -1, 2, -1, -1, 2, -1, -1, 2
i: 1,  1,  2, 2,  2,  3, 3,  3,  4, 4
j: 1,  2,  1, 2,  3,  2, 3,  4,  3, 4
```

Matrix:

$$
\begin{pmatrix}
2 & -1 & 0 & 0 \\
-1 & 2 & -1 & 0 \\
0 & -1 & 2 & -1 \\
0 & 0 & -1 & 2
\end{pmatrix}
$$

---

## SpMV in COO

```c
for(k=0; k<nonzeroes; k++) {
    y[i[k]] += a[k] * x[j[k]];
}
```

### Disadvantages

- Many memory accesses (~5 per iteration)
- Possibly random access patterns
- Low arithmetic intensity

---

# Compressed Row Storage (CRS)

Arrays:

- `a[k]` → non-zero values
- `j[k]` → column indices
- `start[i]` → pointer to start of row $i$

Example:

```
start: 0 2 5 8 10
```

---

## SpMV in CRS

```c
for(i=0; i<n; i++) {
    for(k=start[i]; k<start[i+1]; k++)
        y[i] += a[k] * x[j[k]];
}
```

---

## Arithmetic Intensity (CRS)

Per non-zero:

- read `j[k]` (4 bytes)
- read `x[j[k]]` (4/8 bytes)
- read `a[k]` (4/8 bytes)
- read/write `y[i]`
- 1 fused multiply-add

≈ 1–2 FLOPs per 12–20 bytes.

→ Memory bound.

---

# Variants of CRS

## Compressed Column Storage (CCS)

- Same as CRS but rows and columns exchanged.
- Used in Harwell–Boeing format.

## Block CRS

- Store small dense blocks (e.g. $2\times2$, $4\times4$)
- Better SIMD utilization.

### CRS and SIMD Issues

- Vectorization over k-loop difficult.
- Non-contiguous access to $x$.
- Possible race conditions for $y$.
- Low arithmetic intensity.

---

# Incremental CRS

Define linearized index:

$$
\tilde{j} = (i-1)n + (j-1)
$$

Store increments:

```
inc[k]
```

Compute indices incrementally.

Advantage:

- Avoids `start[i]`
- Can be faster (Bisseling)
- Especially useful if $K < n$

---

# ELLPACK Format (Rectangular Storage)

Assume at most $k_{\max}$ non-zeros per row.

Store:

- Values: $a_{ik}$ in $n \times k_{\max}$ array
- Column indices: $j_{ik}$

Very regular layout → good for vectorization.

---

## SpMV in ELLPACK

### Row-oriented

```c
for(i=0; i<n; i++)
    for(k=0; k<kmax; k++)
        y[i] += a[i][k] * x[j[i][k]];
```

### Column-oriented

```c
for(k=0; k<kmax; k++)
    for(i=0; i<n; i++)
        y[i] += a[i][k] * x[j[i][k]];
```

Advantages:

- Long inner loop
- Vector access to `y`, `a`, `j`
- Supports SIMD and pipelining

Requires hardware support for scattered access to `x`.

---

# Jagged Diagonal Storage (JDS)

Procedure:

1. Sort rows by decreasing number of non-zeros.
2. Store ELLPACK-style arrays column-wise.
3. Omit zero entries.
4. Maintain array `start[k]` for diagonal offsets.

---

## SpMV in JDS

```c
for(k=0; k<kmax; k++)
    for(i=0; i<start[k+1]-start[k]; i++)
        y[i] += a[start[k]+i] * x[j[start[k]+i]];
```

Note:

- Result vector $y$ reordered.
- Good vectorization potential.

---

# Key Observations

Sparse matrix-vector multiplication (SpMV):

- Very low arithmetic intensity.
- Typically memory-bandwidth bound.
- Performance dominated by:
  - Memory layout
  - Cache behavior
  - Vectorization capability

Choice of storage format:

- COO → simple, flexible
- CRS → standard general-purpose
- Block CRS → better SIMD
- ELLPACK → regular, good for GPUs
- JDS → improves vectorization

---

# Reference

Rob H. Bisseling:  
*Parallel Scientific Computing – A Structured Approach using BSP and MPI.*  
Oxford University Press, 2004.