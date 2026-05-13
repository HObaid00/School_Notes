## Dwarf #5 – Structured Grids  
Winter 2025/2026  

---

# 1. Structured Grids – Characterisation

- Regular construction of points/elements
- Geometric & topological information derivable
- Memory addresses easily computed

---

# 2. Types of Structured Grids

## Regular Grids

- Cartesian grids (rectangles / cuboids)
- Triangular meshes
- Row-major or column-major storage

---

## Transformed Grids

- Map unit square to domain:
  $$
  (\xi(x,y), \eta(x,y))
  $$

Variants:

- Algebraic
- PDE-based transformation

---

## Composite Structured Grids

- Domain split into simpler subdomains
- Conforming or overlapping (chimera grids)

---

## Block Structured Grids

- Logically rectangular subdomains
- Fit together in unstructured way
- Popular in CFD

---

# 3. Adaptive Grids

## Block Adaptive

- Entire blocks refined
- Efficient but limited adaptivity

## Recursive (Quadtree/Octree)

- Recursive subdivision
- Tree structures
- Flexible but complex traversal

---

# 4. Stencil Computations

General stencil update:

$$
u_{i,j}^{new}
=
\text{stencil}(u_{i-1,j}, u_{i+1,j}, u_{i,j-1}, u_{i,j+1})
$$

Example (Jacobi, 5-point stencil):

$$
u_{i,j}^{new}
=
\frac{1}{4}
(
u_{i-1,j}
+
u_{i+1,j}
+
u_{i,j-1}
+
u_{i,j+1}
)
$$

---

# 5. Sparse Matrix Equivalence

Stencil ↔ Sparse matrix:

$$
u^{new} = A u^{old}
$$

- Nonzeros correspond to stencil weights
- Much less storage needed than full matrix

---

# 6. PRAM Parallelization

## Jacobi

- Exclusive write
- Exclusive read
- Fully parallel

## Gauss–Seidel

- Data dependencies
- Limited parallelism
- Compiler issues for vectorization

---

## Red-Black Gauss–Seidel

- Split grid into two colors
- Two sweeps
- Eliminates dependencies
- Good for GPUs

---

# 7. Distributed Memory

## Domain Decomposition

- 1D slices
- 2D blocks
- 3D cuboids
- Patch-based

Goal:

- Neighbours on same processor
- Minimize communication boundary

---

# 8. Ghost Cells

- Replicate neighbour data
- Exchange after each iteration
- Multiple layers possible

Communication:

- Direct neighbours
- Or multi-step exchange to avoid diagonal messaging

---

# 9. BSP Model for Cartesian Grid

Assume:

- $n^d$ points per processor
- $c$ flops per point

Computation:

$$
c \cdot n^d
$$

Communication:

$$
2d \cdot n^{d-1}
$$

Total cost (diagonal scheme):

$$
c n^d + 2d (n+1)^{d-1} g + l
$$

d-step scheme:

$$
c n^d + d(2(n+2)^{d-1} g + l)
$$

---

# 10. Scalability

Typically:

- Excellent weak scaling
- Memory-bound
- Low arithmetic intensity

Challenges:

- Adaptive refinement
- Complex geometries
- Science per flop