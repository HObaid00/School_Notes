The tile-oriented LU decomposition, as discussed in the lectures, finds matrices \(L\) and \(U\) such that \(LU = A\) for a given matrix \(A\), where \(L\), \(U\), and \(A\) are given in the following formulation:

$$
\begin{pmatrix}
\hat{L}_{11} & 0 & 0 & \cdots & 0 \\
L_{21} & \hat{L}_{22} & 0 & \cdots & 0 \\
L_{31} & L_{32} & \hat{L}_{33} & \cdots & 0 \\
\vdots & \vdots & \vdots & \ddots & 0 \\
L_{n,1} & L_{n,2} & L_{n,3} & \cdots & \hat{L}_{n,n}
\end{pmatrix}
\begin{pmatrix}
\tilde{U}_{11} & U_{12} & U_{13} & \cdots & U_{1,n} \\
0 & \tilde{U}_{22} & U_{23} & \cdots & U_{2,n} \\
0 & 0 & \tilde{U}_{33} & \cdots & U_{3,n} \\
\vdots & \vdots & \vdots & \ddots & U_{n-1,n} \\
0 & 0 & 0 & \cdots & \tilde{U}_{n,n}
\end{pmatrix}
=
\begin{pmatrix}
A_{11} & A_{12} & A_{13} & \cdots & A_{1,n} \\
A_{21} & A_{22} & A_{23} & \cdots & A_{2,n} \\
A_{31} & A_{32} & A_{33} & \cdots & A_{3,n} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
A_{n,1} & A_{n,2} & A_{n,3} & \cdots & A_{n,n}
\end{pmatrix}
$$

In this notation, all matrices $(\tilde{L}_{ii})$ are lower-triangular and all matrices $( \tilde{U}_{ii} )$ are upper-triangular.

Tiled LU-decomposition makes use of four basic operations on tiles \( A_{ij} \), etc.:

- **LUdecomp$(A_{ii})$**: find $\hat{L}_{ii}$ and  $\tilde{U}_{ii}$ such that  $\hat{L}_{ii}\tilde{U}_{ii} = A_{ii}$

- **findLeft$(A_{ij})$**: for given  $\tilde{U}_{jj}$ and  $A_{ij}$, find  $L_{ij}$, such that   $L_{ij}\tilde{U}_{jj} = A_{ij}$

- **findRight($A_{ij}$)**: for given $\hat{L}_{ii}$ and $A_{ij}$, find $U_{ij}$, such that  $\hat{L}_{ii}U_{ij} = A_{ij}$

- **tileUpdate($A_{ij}, k$)**:  $A_{ij} := A_{ij} - L_{ik}U_{kj}$

Recall that all operations are performed “in place”, such that for the find left/right operations, \(L_{ij}\) and \(U_{ij}\) overwrite \(A_{ij}\) (similar for LU-decomposition on a tile).

---

### a) State (in pseudo-code or in plain words) which tile operations need to be executed to achieve the following situation:

$$
\begin{pmatrix}
\hat{L}_{11} & 0 & 0 & \cdots & 0 \\
L_{21} & I & 0 & \cdots & 0 \\
L_{31} & 0 & I & \cdots & 0 \\
\vdots & \vdots & \vdots & \ddots & 0 \\
L_{n,1} & 0 & 0 & \cdots & I
\end{pmatrix}
\begin{pmatrix}
\tilde{U}_{11} & U_{12} & U_{13} & \cdots & U_{1,n} \\
0 & A^{*}_{22} & A^{*}_{23} & \cdots & A^{*}_{2,n} \\
0 & A^{*}_{32} & A^{*}_{33} & \cdots & A^{*}_{3,n} \\
\vdots & \vdots & \vdots & \ddots & A^{*}_{n-1,n} \\
0 & A^{*}_{n,2} & A^{*}_{n,3} & \cdots & A^{*}_{n,n}
\end{pmatrix}
$$

---

### Example solution:

1. **LUdecomp($A_{11}$)**, i.e., find $\hat{L}_{11}$ and $\tilde{U}_{11}$ such that  $\hat{L}_{11}\tilde{U}_{11} = A_{11}$

2. for $i = 2, \ldots, n$: **findLeft($A_{i1}$)**, i.e., determine all $L_{i1}$

3. for $j = 2, \ldots, n$:  **findRight($A_{1j}$)**, i.e., determine all $U_{1j}$

4. for $i = 2, \ldots, n$:  
	   for $j = 2, \ldots, n$:  **tileUpdate($A_{ij}, 1$)**

i.e., update all “trailing” tiles.

---
### b) State the main assumption that the BSP model applies on computation and communication between CPUs. Explain the concept of *supersteps* in the BSP model.

---
### Example Solution
Compare lecture slides:
* we consider multiple CPUs (as many as needed/desired), each with private memory
* CPUs are connected via a point-to-point network (each processor can send to each other)
* BSP algorithms are organised as a sequence of supersteps
* each superstep consists of three phases:
	1. Computation(on the local memory)
	2. Communication (send messages between CPUs)
	3. Synchronization (wait until all messages have arrived)
![[Pasted image 20260409130236.png|697]]
---
### c) Describe the BSP supersteps that are needed to implement your tiled *LU* decomposition from exercise a) according to the BSP model.
	Assume that you use n CPUs and thatm at start, CPU #i contains all matrix tiles $A_{i,j}$

### Example solution:
There are two possible approaches to deal with the $\text{findRight}$ operations.
#### Approach #1: strict "owner computes"
In this approach, we always compute a tile operations where the respective $A$ block is loacated, even if that leads to sequential computations.

$\text{Superstep \#1}$:
1. Compute:
	CPU $\#1$ executes $\text{LUdecomp}(A_{11});$ all other CPUs idle)

2.	CPU $\text{\#1}$ sends tile with $\hat{L}_{11}$ and $\tilde{U}_{11}$ (i.e., $A_{i,j}$) to all processors $2, ..., n$ 
	*or: formulate via "get/receive"-type commands:*
	all CPUs $2, ..., n$ get/receive tile with $\hat{L}_{11}$ and $\tilde{U}_{11}$ (i.e. $A_{11}$) from CPU $\#1$ 

1. Synchronize

Superstep #2:
1. Compute:
in parallel: execute findLeft(Ai,1 ) on CPU #i for all i = 2, . . . , n
sequentially, only on CPU #1: compute all findRight(A1,j ) for all j = 2, . . . , n
2. Communicate:
CPU#1 needs to send all computed tiles U1,j (for j = 2, . . . , n) to each CPU#i (for i =
2, . . . , n)
3. Synchronize
The sequential computation of all the findRights on CPU #1 is, of course, unsatisfactory regard-
ing parallelisation. Also the broadcast of all tiles of the first row, U1,j , is very costly.
Superstep #3:
4. Compute:
each CPU (for i = 2, . . . , n) performs the following calculations:
for j = 2, . . . , n: tileUpdate(Aij , 1).
Each tileUpdate(Aij , 1) – and thus each CPU#i – requires Li,1 (has been computed on
CPU#i) and U1,j (normally located on CPU#1, sent to CPU#j during Superstep #2).