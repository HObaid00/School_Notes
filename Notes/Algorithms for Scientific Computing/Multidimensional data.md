## Challange #1
* sampling in 1D, 2D, 3D requires $n, \ n^2, \ n^3$ points (in general $n^d$)
* how about problems, where $d > 3$ (or $d > 10$, or $d > 100$)?
**"Sparse Grids:"**
![[Pasted image 20260413145104.png|520]]

**Examples for multi-dimensional data structures:**
* Matrices, tensors
* Image data (image, tomography, movies, ...)
* Discretization based on grids (discretization of physical models / partial differential databases)
* In financialmathematics: baskets of stocks/options/...

**Also:**
anything that is forced to become (i.e., turned into) multidimensional data
-> classification and learning

---

## Challenge #2: linearization/sequentialization
* Storage of data structures in memory
* Data processing (traversal)

**Demands on linearization ("efficiency"):
* Maintain neighborhood $\Rightarrow$ locality of data, "clustering"
* Simple, fast computation of indices
* "Continuity", regularity
* Symmetry w.r.t single dimensions 

**Space-Filling Curves and Octrees:
* functions on structured adaptive grids
* ordered by space-filling curves

![[Pasted image 20260413150034.png|529]]

