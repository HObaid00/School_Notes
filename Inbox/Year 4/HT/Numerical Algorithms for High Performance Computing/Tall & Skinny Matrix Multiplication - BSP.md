Consider the following multiplication of dense matrices
$$\Large
\begin{pmatrix}
A_{11} & A_{12} & \cdots & A_{1n} \\
A_{21} & A_{22} & \cdots & A_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
A_{n1} & A_{n2} & \cdots & A_{nn}
\end{pmatrix}
\begin{pmatrix}
B_1 \\
B_2 \\
\vdots \\
B_n
\end{pmatrix}
=
\begin{pmatrix}
C_1 \\
C_2 \\
\vdots \\
C_n
\end{pmatrix} \ (2)
$$
where all $A_{ij}$ , $B_j$ , $C_i$ are $\text{b × b}$ matrix blocks. Hence, with $N = nb$, A is an $\text{N × N}$ -matrix and $B$ and $C$ are $\text{N × b}$ matrices. The elements of the matrix $A$ can be computed on the fly using
the function $compA()$  which performs $f$ floating point operations per call. A one-level blocking approach to compute equation above is implemented in the following algorithm:
```
TSM_Mult(B:Matrix[n], C:Matrix[n]) {
	// two nested loops over b*b blocks
	for i from 0 to n-1 do
		for j from 0 to n-1 do {
			// multiplication of b*b block matrices:
			for ii from 1 to b do
				from kk from 1 to b do
					for jj from 1 to b do
						C[i*b+ii, kk] =
							C[i*b+ii, kk] + compA(i*b+ii, j*b+jj)*B[j*b+jj, kk] 
		}
}
```

a) Describe a parallel algorithm using the Bulk Synchronous Parallelism (BSP) model that computes this $\text{tall \& skinny}$ matrix multiplication on n processors. Assume that a processor cannot store more than three $\text{b × b}$ matrix blocks at any time. Define the exact sequence of performed super steps.

**Example solution:** 
* We parallelized over the i-loop. Processor $i$ shall permanently store the matrix blocks $B_i$ and $C_i$ has to fetch (and store) the matrix block $B_j$ in each super step.
* We modify the j-loop to avoid that all processors always access the same matrix blocks $B_j$; as processor $i$ holds $B_i$ in the beginning, each processor $i$ starts its loop with $j = 1$ (cmp. Cannon's Algorithm).
* We need to do n super steps, each of which consists of three operations:
	1. computation: perform block multiplication $C_i :=  C_i + A_{i,j} B_j$ (note that for the first loop iteration j = i and thus all operands of $C_i := C_i +A_{i,i} \ B_i$ are local on processor i)
	2. communication: get the next block $B_{j+1}$ from processor $B_{j+1}$
	3. Synchronize: wait until all communication operations have been finished.
	In the first super step, we set $j := i$, and then increment $j$ after each super step. All increments (incl. the one in the communication) step should be "modulo n". The last superstep fetches block $B_i$ on each processor $i$, which is not necessary for the computation, but restores the initial configuration that each processor holds $B_i$.

b) For your algorithm in a), use the BSP model to derive an estimate of the computation time on $n$ processors.

**Example Solution**
	In each superstep, we perform the following operations:
		1. computation: in each innermost loop body $f$ operations to compute the $A$ element, plus 1 addition and 1 multiplication -> $(f+2)b^3$ operations
		2. communicate: recieve $b^2$ floating point values (for $B_{j+1}$)
		3. synchronize
	Hence each superstep requires a computation time of $\gamma (f+2)b^3 +\beta b^2 + \lambda$, where $\gamma$, $\beta$ and $\lambda$ are the relative costs of computation, communication and synchronization. The total computation time is therefore 
$$\Large
n(\gamma(f+2)b^3 + \beta b² + \lambda)
$$
