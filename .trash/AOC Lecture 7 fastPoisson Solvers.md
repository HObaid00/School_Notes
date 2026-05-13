# Algorithms of Scientific Computing  
## Fast Poisson Solvers  
*Michael Bader, Technical University of Munich, Summer 2026* :contentReference[oaicite:0]{index=0}

---

## Spectral Methods

General idea: solve problems in **frequency space instead of physical space**.

- transform problem → frequency domain  
- solve easier algebraic problem  
- transform solution back  

Tools:
- DST / DCT  

Applications:
- Fast Poisson solvers  
- JPEG compression  
- Signal filtering  

---

## Part I: Heat Transfer and Poisson Equation

### Modeling Heat Transfer

Goal: compute temperature distribution $T$ in an object.

Assumptions:
- boundary temperatures known  
- heat sources present  
- material parameters (e.g. $k$)  

Empirical law:
$$\Large
q \propto k \cdot \Delta T
$$

---

## Finite Volume Model

- domain: rectangular plate  
- discretized into grid cells of size $h_x \times h_y$  
- temperature per cell: $T_{ij}$  

Heat flow across edges depends on:
- temperature difference  
- edge length  

Example (left edge):

$$\Large
q^{(\text{left})}_{ij} = k_x (T_{ij} - T_{i-1,j}) \, h_y
$$

Total heat flow:

$$\Large
q_{ij} =
k_x (T_{ij} - T_{i-1,j}) h_y
+
k_x (T_{ij} - T_{i+1,j}) h_y
+
k_y (T_{ij} - T_{i,j-1}) h_x
+
k_y (T_{ij} - T_{i,j+1}) h_x
$$

---

## Temperature Equilibrium

Energy conservation:

$$
q_{ij} + F_{ij} = 0
$$

Source term:

$$
F_{ij} = f_{ij} h_x h_y
$$

Leads to:

$$\Large
f_{ij} h_x h_y =
- k_x h_y (2T_{ij} - T_{i-1,j} - T_{i+1,j})
- k_y h_x (2T_{ij} - T_{i,j-1} - T_{i,j+1})
$$

---

## Discrete Equation

Divide by $h_x h_y$:

$$\Large
f_{ij} =
- \frac{k_x}{h_x} (2T_{ij} - T_{i-1,j} - T_{i+1,j})
- \frac{k_y}{h_y} (2T_{ij} - T_{i,j-1} - T_{i,j+1})
$$

This yields a **linear system**.

Boundary handling:
- fixed temperature (Dirichlet)  
- fixed heat flow (Neumann)  

---

## From Discrete to Continuous

Replace:

$$
k_x \to \frac{k}{h_x}, \quad k_y \to \frac{k}{h_y}
$$

Then:

$$\Large
f_{ij} =
- \frac{k}{h_x^2}(2T_{ij} - T_{i-1,j} - T_{i+1,j})
- \frac{k}{h_y^2}(2T_{ij} - T_{i,j-1} - T_{i,j+1})
$$

As $h_x, h_y \to 0$:

$$\Large
f(x,y) = -k \left(
\frac{\partial^2 T}{\partial x^2}
+
\frac{\partial^2 T}{\partial y^2}
\right)
$$

This is the **Poisson equation**:

$$\Large
- k \Delta T(x,y) = f(x,y)
$$

---

## Spectral Methods for PDE

Use transforms (DST/DCT) to solve PDEs:

- transform problem → frequency domain  
- solve algebraic equations  
- inverse transform  

Limitations:
- irregular domains  
- variable coefficients  

---

## Part II: Fast Poisson Solver

### Discrete System

2D system:

$$\Large
- u_{i-1,j} - u_{i+1,j} + 4u_{ij} - u_{i,j-1} - u_{i,j+1} = f_{ij}
$$

1D case:

$$\Large
- u_{n-1} + 2u_n - u_{n+1} = f_n, \quad n=1,\dots,N-1
$$

with:

$$
u_0 = u_N = 0
$$

---

## Applying the Sine Transform

Represent:

$$\Large
u_n = 2 \sum_{k=1}^{N-1} U_k \sin\left(\frac{\pi n k}{N}\right)
$$

$$\Large
f_n = 2 \sum_{k=1}^{N-1} F_k \sin\left(\frac{\pi n k}{N}\right)
$$

Key idea:
- sine functions are **eigenvectors of the discrete Laplacian**
- transforms diagonalize the system  

---

## Transforming the System

Insert expansions into:

$$
- u_{n-1} + 2u_n - u_{n+1} = f_n
$$

Use identities:

$$\Large
\sin(A+B) = \sin A \cos B + \cos A \sin B
$$

$$\Large
\sin(A-B) = \sin A \cos B - \cos A \sin B
$$

Key simplification:

$$\Large
\sin(A+B) + \sin(A-B) = 2 \sin(A)\cos(B)
$$

---

## Simplified Equation

After simplification:

$$\Large
2 \sum_{k=1}^{N-1}
U_k \sin\left(\frac{\pi n k}{N}\right)
\left(1 - \cos\left(\frac{\pi k}{N}\right)\right)
=
\sum_{k=1}^{N-1}
F_k \sin\left(\frac{\pi n k}{N}\right)
$$

---

## Solving for Coefficients

Matching coefficients gives:

$$\Large
2 U_k \left(1 - \cos\left(\frac{\pi k}{N}\right)\right) = F_k
$$

Thus:

$$\Large
U_k =
\frac{F_k}{2 - 2\cos\left(\frac{\pi k}{N}\right)}
$$

---

## Fast Poisson Solver Algorithm

### Step 1: Forward DST

$$\Large
F_k =
\frac{1}{N}
\sum_{n=1}^{N-1}
f_n \sin\left(\frac{\pi n k}{N}\right)
$$

### Step 2: Solve in Frequency Space

$$\Large
U_k =
\frac{F_k}{2 - 2\cos\left(\frac{\pi k}{N}\right)}
$$

### Step 3: Inverse DST

$$\Large
u_n =
2 \sum_{k=1}^{N-1}
U_k \sin\left(\frac{\pi n k}{N}\right)
$$

---

## Computational Cost

- DST: $O(N \log N)$  
- coefficient computation: $O(N)$  

Total:

$$\Large
O(N \log N)
$$

Comparison:
- 1D direct solver: $O(N)$  
- advantage appears in 2D / 3D  

---

## Applicability Conditions

The method requires:

- boundary conditions:$$\Large
  u_0 = u_N = 0
  $$
- rectangular domain  
- Cartesian grid  
- constant material parameters  

---

## Key Insight

The sine transform diagonalizes the discrete Laplacian operator, converting a coupled linear system into independent scalar equations in frequency space. This enables efficient solution using FFT-based methods.