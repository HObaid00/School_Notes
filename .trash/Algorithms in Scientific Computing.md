# Lecture 1 Overview and General Remarks

## Turtorials 
* Friday - Friday
* Worksheets with applications
* No bonus points

## Leacture Slides: Color Code For Headers
* Black: for all slides with regular topics
* Green: Summurization
* Red: Advanced topics or outlooks; will not be apart of the exam
* Blue: Background information or fundamental concepts that are already known

## For Comparison: Representation of Scalars - Curcial Ideas:
* Hierarchy (different "value" of digits depending on their position)
* Structure (concept of 0 as a placeholder)
* Adaptivity (e.g., "scientific" notation: $1.7 \cdot 10^4$)

## Representation of Mathematical Functions
Possibility of representation (historical):
* *analytical function:* $f(x) = e^x \ sin(x)$
* tabulated values
	(historical example: logorithms tables; modern: rastered data/sampling)
* interpolation (also piecewise):
	(polygonal chain/curve, polynomial interpolation, spline interpolation, trigonometrical interpolation, ...)

**Goals: access and use information efficiently!**
* more compact storage
* identification of certain properties (information)
* more efficient algorithms for processing/computations

**Key Formula: ("coefficients and basis funtions)**
$$\Large
f(x) ≃ \sum c_i \phi_i(x)
$$
## Topic #1: Frequency Domain, Spectral Data, etc.
**Represent data as overlapping waves of different frequencies:**
* analyse frequencies and amplitudes instead of samples
* requires respective transforms: Fourier, Wavelets, etc.

![[Pasted image 20260413144737.png]]

## Topic #2: Multi-Dimensional Data
### Challenge #1: "curse of dimensionality"
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

### Challenge #2: linearization/sequentialization
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

## Topic #3: Adaptivity
**Use different ("adaptive") resolution in areas of interest:
* structured (recursive) or unstructured refinement?
* motivates recursive algorithms and hierarchical data structures

![[Pasted image 20260413150311.png]]

## Recursive Algorithms and Hierarchical Data Structures
**Algorithmic aspects in scientific computing:
* *Recursive and hierarchical:* w.r.t algorithms (partitioning of problem) and data structures (trees, object orientation)
* Adaptive: invest effort, where largest benefit can be achieved
* *"Optimal Complexity"* ($O(h)$ and $O(n)$): high approximation order, etc.
* *Distributed:* Computing on parallel and distributed systems
* *Hardware-oriented*: -> High Performance Computing
> Generally applicable concepts and ideas


## Interpolation/Representation of Data
**Given:
* a set of values: $f_i, \ f_{ij},  \dots \ \text{(1D, 2D, ...)}$
* at grid/sampling points $x_i, \ x_{ij}, \ \dots$
**Wanted:
* function $f(x) = \sum a_i \phi_i(x)$ such that $f(x_i) = f_i$ (similar in 2D)
* we need to compute the coefficients $a_i$
**Important aspects:
* solution depends on clever choice of the basis functions $\phi_i$ (recall: Lagrange/Newton interpolation)
* can we skip coefficients/basis functions a-priori/a-posteriori?
>	adaptivity, compression, etc.

## Recall: Interpolation Problem
For given values $b_i$ and points $x_i$ ($i=1, \ \dots \ , \ n$) find a function $f(x)$, such that:
$$\Large
f(x_i) = b_i \ \forall \ i = 1, \ ..., \ n \quad \text{where} f(x_i) = \sum_{j=1}^n \ a_j \ g_j(x_i) 
$$
The functions $g_j(x)(j=1, \ \dots, \ n)$ are suitably selected (polynomials, e.g.).

With $G_{ij} := g_j(x_i)$, we can write the problem as a system of linear equations:
$$\Large
\begin{array}a
\sum_{j=1}^n \ a_j g_j(x_i) = n_i \forall \ i=1, \ \dots, \ n \\
\iff \sum_{j=1}^n \ G_{ij}a_j \forall \ i=1, \ \dots, \ n
\end{array}
$$
Corresponds to solving a linear system of equations: $\Large Ga \ = \ b$

## Approximation of Data
**Given:
* a set of values: $f_i, \ f_i{ij}, \ \dots$ (1D, 2D, ...)
* at points $x_i, x_{ij}, \ \dots$
**Wanted:
* function $f(x) = \sum a_i \phi_i(x)$ such that $\sum (f_i - f(x_i))^2$ is minimal
* we need to compute the coefficient $a_i$
**Important aspects:
* typically more data $f_i$ than coefficients (overdetermined)
* solution depends on clever of the basis function $\phi_i$ -> how many functions, and how should they look like?
* related to classification and learning("big data")

---
## Recall: Approximation Problem

For given values $b_i$ and points $x_i$ $(i = 1, \dots, m)$ find a function $f(x)$, such that:

$$\Large
f(x_i) \approx b_i \quad \text{for all } i = 1, \dots, m
$$

where

$$\Large
f(x_i) = \sum_{j=1}^{n} a_j g_j(x_i), \quad \text{with } m > n
$$

---

We find the best approximation by minimising the quadratic error:

$$\Large
\sum_{i=1}^{m} (f(x_i) - b_i)^2 \; \overset{!}{=} \; \min
\;\;\Longleftrightarrow\;\;
\sum_{i=1}^{m} \left( \sum_{j=1}^{n} a_j g_j(x_i) - b_i \right)^2 \; \overset{!}{=} \; \min
$$

---

We set all derivatives w.r.t. our variables $a_k$ to $0$  
(with $G_{ij} := g_j(x_i)$ for all $k = 1, \dots, n$):

$$\Large
\frac{\partial}{\partial a_k}
\left(
\sum_{i=1}^{m}
\left( \sum_{j=1}^{n} a_j G_{ij} - b_i \right)^2
\right)
=
\sum_{i=1}^{m}
\frac{\partial}{\partial a_k}
\left( \sum_{j=1}^{n} a_j G_{ij} - b_i \right)^2
\overset{!}{=} 0
$$

$$\Large
\Longleftrightarrow
\sum_{i=1}^{m}
2 \left( \sum_{j=1}^{n} a_j G_{ij} - b_i \right) G_{ik} = 0
$$

$$\Large
\Longleftrightarrow
\sum_{i=1}^{m} G_{ik} \sum_{j=1}^{n} a_j G_{ij}
=
\sum_{i=1}^{m} G_{ik} b_i
$$

---

Corresponds to solving a linear system of equations:

$$\Large
G^T G a = G^T b
$$
---
## Approximation with Regularization

Given:
- a set of values: $f_i, f_{ij}, \dots$ (1D, 2D, $\dots$)
- at points $x_i, x_{ij}, \dots$

Wanted:
- function $f(x) = \sum a_i \phi_i(x)$ such that

$$\Large
\sum (f_i - f(x_i))^2 + \gamma \|L f\| \;\; \text{is minimal}
$$

with $L f = f'$, $L f = f''$, or similar.

- compute coefficients $a_i$ (depend on parameter $\gamma$)

**Important aspects:**
- more or less data $f_i$ available than required (over- or underdetermined)
- frequent approach to predict value $f(x)$  
  → related to classification and learning (“big data”)
- solution depends on clever choice of the basis functions $\phi_i$  
  → how many functions, and how should they look like?

---

## Find / Approximate a Function

Problem:
- approximate a function that cannot be represented exactly: $f(x) \approx b(x)$
- using a representation $f(x) = \sum a_i \phi_i(x)$

Leads to question of approximation between functions:

$$\Large
\|f\|^2 = \int f(x)^2 \, dx
$$

Minimize:

$$\Large
\left\| b(x) - \sum a_i \phi_i(x) \right\|^2
$$

---

### Orthogonality Argument

- norm derived from dot product on functions:

$$\Large
\langle f, g \rangle = \int f(x) g(x) \, dx
$$

- demand that the error is orthogonal to all test functions:

$$\Large
\int v(x)\left( b(x) - \sum a_i \phi_i(x) \right) dx = 0 \quad \text{for all } v
$$

---

## Find / Approximate a Function (2)

More interesting setup:
- solve a partial differential equation, e.g.:

$$\Large
\frac{\partial^2}{\partial x^2} f(x) = b(x)
$$

(with initial and boundary conditions)

Wanted:
- function $f(x) = \sum a_i \phi_i(x)$ that “solves” the equation
- depending on choice of $\phi_i(x)$, only an approximate solution may be possible

---

### Leads to Finite Element Methods

- demand:

$$\Large
\int v(x)\left( b(x) - \frac{\partial^2}{\partial x^2} f(x) \right) dx = 0 \quad \text{for all } v
$$

- solution depends on:
  - choice of basis functions $\phi_i$
  - choice of test functions $v$

→ leads to a system of equations for $a_i$

---

# What are our Algorithms?

*(Section header slide)*

---

# Schedule

## Fast Fourier Transform
- discrete Fourier transform as 2D, 3D interpolation
- FFT as divide-and-conquer algorithm
- transform for data compression (images, audio, video)

## Hierarchical Basis and Sparse Grids
- adaptive integration and Archimedes’ quadrature
- hierarchical basis functions
- curse of dimensionality → sparse grids
- wavelets

## Space Trees and Space-Filling Curves
- sequential data structures and traversal of octrees
- definition and construction of space-filling curves
- adaptivity vs. parallelisation and partitioning

---
