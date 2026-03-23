## Dwarf #6 – Unstructured Grids  

Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# Dwarf #6 – Unstructured Grids

1. dense linear algebra  
2. sparse linear algebra  
3. spectral methods  
4. N-body methods  
5. structured grids  
6. unstructured grids  
7. Monte Carlo  

Copy picture from **Slide 2**.

---

# Part I: Unstructured Grid Generation

## Unstructured Grids – Characterisation

- (almost) no restrictions on grid generation → maximum flexibility  
- explicit storage of basic geometric and topological information  
  → usually complicated data structures  

Example: unstructured mesh of a subduction zone for earthquake simulation.

![[Pasted image 20260303120057.png]]

---

## Example: Delaunay Triangulation

Assume: grid points are already given.  
Goal: generate triangular grid cells.

### Delaunay Property

The circumcircle of any triangle does **not** contain any other grid vertex.

Properties:

- leads to triangles with favourable properties  
  → avoids very acute or obtuse angles  
- related to Voronoi diagrams  
- widely used (computer graphics, FEM meshes, etc.)

![[Pasted image 20260303120015.png]]

---

## Delaunay Triangulation and Voronoi Diagrams

### Algorithm

1. Construct Voronoi region around each grid point:

$$
V_i = \{ P : \|P - P_i\| < \|P - P_j\| \ \forall j \neq i \}
$$

2. Connect points from adjacent Voronoi regions.  
3. This yields a set of disjoint triangles  
   (tetrahedra in 3D).

![[Pasted image 20260303120151.png]]

---

## Example: Advancing Front Methods

- Generates both grid points and grid cells.  
- Advance a *front* step-by-step towards the interior.  
- Start from the boundary (initial front).

![[Pasted image 20260303120220.png]]

---

## Advancing Front Methods – Algorithm

1. Choose an edge on the current front, say $PQ$.  
2. Create a new point $R$ at equal distance $d$ from $P$ and $Q$.  
3. Determine all grid points within a circle around $R$ (radius $r$).  
4. Order these points by distance from $R$.  
5. Form triangles with $P$ and $Q$; select one candidate.  
6. Add triangle to grid (if no intersections etc.).  
7. Update triangulation and front line.

Copy illustrations from **Slides 9–10**.

---

# Part II: Finite Element Methods on Unstructured Grids

## Recall: Finite Element Discretisation

### 1. Weak Formulation

Given:
$$
Lu = f
$$

Multiply with test function $v$:

$$
\int vLu \, dx = \int vf \, dx
$$

Example (Poisson):

$$
u'' = f
$$

Weak form:
$$
\int v' u' \, dx = \int vf \, dx
$$

---

### 2. Approximation in Finite-Dimensional Space

Compute numerical solution:

$$
u_h = \sum_j u_j \varphi_j(x), \quad 
\text{span}\{\varphi_1, \dots, \varphi_J\} = W_h
$$

---

### 3. Choose Basis Functions

(e.g. piecewise linear hat functions)

Leads to system:

$$
\int \psi_i L\left( \sum_j u_j \varphi_j(x) \right) dx
=
\sum_j u_j 
\underbrace{\int \psi_i L\varphi_j(x) dx}_{=: A_{ij}}
=
\int \psi_i f \, dx
\quad \forall \psi_i
$$

---

## Element Stiffness Matrices

For complicated meshes:

Questions:

- How to set up the system efficiently?
- Can stencil notation still be used?

→ Switch to element stiffness matrices.

![[Pasted image 20260303120254.png]]

---

## Element-Oriented Computation

Domain subdivision:

$$
\Omega = \Omega^{(1)} \cup \Omega^{(2)} \cup \dots \cup \Omega^{(n)}
$$

Often basis functions are defined element-wise.

Example:

$$
A_{ij}
=
\int_\Omega \nabla \varphi_j \cdot \nabla \varphi_i \, dx
=
\sum_k 
\underbrace{\int_{\Omega^{(k)}} 
\nabla \varphi_j \cdot \nabla \varphi_i \, dx}_{=: A^{(k)}_{ij}}
$$

Thus:

$$
A = \sum_k A^{(k)}
$$

Similarly for RHS:

$$
b_i = \int_\Omega f \varphi_i dx
=
\sum_k \int_{\Omega^{(k)}} f \varphi_i dx
$$

![[Pasted image 20260303120329.png]]

---

## Example: 1D Poisson

Let:
$$
\Omega = [0,1]
$$

Split into elements:
$$
\Omega^{(k)} = [x_k, x_{k+1}]
$$

Element stiffness matrix:

$$
A^{(k)} =
\frac{1}{h}
\begin{pmatrix}
1 & -1 \\
-1 & 1
\end{pmatrix}
$$

For three unknowns:

$$
A^{(1)} + A^{(2)} =
\frac{1}{h}
\begin{pmatrix}
1 & -1 & 0 \\
-1 & 1 & 0 \\
0 & 0 & 0
\end{pmatrix}
+
\frac{1}{h}
\begin{pmatrix}
0 & 0 & 0 \\
0 & 1 & -1 \\
0 & -1 & 1
\end{pmatrix}
$$

Stencil form:

$$
\frac{1}{h}[-1 \quad 2 \quad -1]
$$

---

## Example: 2D Poisson

2D Cartesian grid, bilinear basis functions.

Element stiffness matrix:

$$
A^{(k)} =
\begin{pmatrix}
2 & -\frac12 & -\frac12 & -1 \\
-\frac12 & 2 & -1 & -\frac12 \\
-\frac12 & -1 & 2 & -\frac12 \\
-1 & -\frac12 & -\frac12 & 2
\end{pmatrix}
$$

After assembly → 9-point stencil:

$$
\begin{bmatrix}
-1 & -1 & -1 \\
-1 & 8  & -1 \\
-1 & -1 & -1
\end{bmatrix}
$$

Exercise: derive and assemble global matrix.

---

## Typical FEM Workflow

1. Choose grid ($\Omega^{(k)}$)
   - quadrilaterals, triangles, tetrahedra, etc.
2. Set up basis functions.
3. Compute element stiffness matrices:

$$
A^{(k)}_{ij} = 
\int_{\Omega^{(k)}} 
\nabla \varphi_j \cdot \nabla \varphi_i dx
$$

4. Assemble global matrix $A$ and RHS.
   - Choose sparse matrix storage.
5. Call (parallel) solver:
   $$
   Ax = b
   $$
   (e.g. communication-avoiding CG)

---

## Assembly of Global Stiffness Matrix

Local matrix $\bar A^{(k)}$ (omit zero rows/columns).

Connection via projection matrix:

$$
A^{(k)} = 
(P^{(k)})^T \bar A^{(k)} P^{(k)}
$$

with

$$
P^{(k)}_{\mu,i} =
\begin{cases}
1 & \text{if } i = \iota^{(k)}(\mu) \\
0 & \text{otherwise}
\end{cases}
$$

Global matrix:

$$
A = \sum_k A^{(k)} 
= \sum_k (P^{(k)})^T \bar A^{(k)} P^{(k)}
$$

Assembly procedure per element:

1. Compute $\bar A^{(k)}$
2. Determine global indices via $\iota^{(k)}$
3. Add nonzeros to $A$

---

## Matrix Assembly on the PRAM

Algorithm:

```
for all elements k in parallel:
    1. compute element stiffness matrix
    2. determine global positions
    3. add contributions to A
```

- Steps 1 & 2 → EREW  
- Step 3 → CRCW possible  
  (multiple elements update same $A_{ij}$)

Example:

- $A_{ii}$ updated by all elements adjacent to vertex $i$
- $A_{ij}$ updated by elements adjacent to edge $(i,j)$

---

## Remedy: Colouring Approach

Idea (similar to Red-Black Gauss-Seidel):

- Colour elements so that elements updating same vertex
  have different colours.
- Process colours sequentially.
- Parallel loop inside one colour.

Example: 2D Cartesian grid, bilinear elements  
→ at most 4 elements per vertex  
→ 4 colours sufficient.

![[Pasted image 20260303120354.png]]

---

## Graph Colouring for Unstructured Grids

Graph representations:

### Standard Graph $(V,E)$

- $V$ = grid vertices  
- $E$ = grid cell edges  

### Dual Graph $(V',E')$

- $V'$ = grid cells  
- $E'$ = adjacency of grid cells  

![[Pasted image 20260303120414.png]]

---

## Matrix Assembly with Graph Colouring

EREW algorithm:

```
for all colours c:
    for all elements k with colour c in parallel:
        1. compute element stiffness matrix
        2. determine global positions
        3. add contributions to A
```

Discussion:

- Effect of multiple passes?
- How many colours needed?
- Parallelism level?

---

# Part III: Unstructured Grid Computations – Distributed Memory

![[Pasted image 20260303120436.png]]

---

## Parallelisation of Unstructured Grids

### Finding Concurrency

- Assembly: element updates in parallel (concurrent write issue).
- Matrix-vector product:
  - parallel SpMV?
  - matrix-free using element matrices?
- Access limited to direct neighbours.

### Efficiency Considerations

- Distribute by elements or unknowns?
- Assembly should be local.

---

## Load Distribution and Communication

Divide grid into partitions:

- One partition per CPU/core.
- Equal computational load → partitions of similar size.
- Minimise communication:
  - minimise number of cells at partition boundaries.

![[Pasted image 20260303120507.png]]

---

## BSP Super-Step

Typical super-step:

1. Perform partition-local update (use ghost cells).
2. Exchange boundary data:
   - send cell-local data at partition boundary.
3. Synchronise.

### Main Influences on Parallel Time

- Load balance (size of largest partition).
- Number of boundary cells.

Copy picture from **Slide 27**.