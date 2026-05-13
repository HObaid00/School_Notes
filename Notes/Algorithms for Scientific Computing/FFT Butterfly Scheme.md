# Butterfly Schema
Consider the formula 
$$\Large
x_n = y_n + \omega_N^n z_n \ \text{ for indices } \ \frac{N}{2}, \dots, N-1:
$$
$$\Large
x_{n+\frac{n}{2}} = y_{n+\frac{n}{2}} + \omega_{N}^{n + \frac{n}{2}} z_{n+\frac{n}{2}} \ \text{ for } \ n = 0, \dots, \frac{N}{2}-1
$$
since $\omega_N^{n + \frac{N}{2}} = -\omega_N^n$ and $y_n$ and $z_n$ have a period of $\frac{N}{2}$, we obtain the so-called **butterfly Scheme:

![[Pasted image 20260421184657.png]]

![[Pasted image 20260421184717.png]]

![[Pasted image 20260421184749.png]]



---
# Recursive Implementation of the FFT
rekFFT(X) ---> x

### (1) Generate vectors Y and Z:
$$\Large
\text{for } \ n=0,\dots, \frac{N}{2} -1: \quad Y_n := X_{2n} \quad \text{and } \ Z_n:= X_{2n+1}
$$
### (2) compute 2 FFTs of half size:
$$\Large
rekFFT(Y) \rightarrow y \quad     \text{and} \quad    rekFFT(Z) \rightarrow z
$$
### (3) combine with "butterfly scheme":
$$\Large
\text{for } \ k = 0,\dots, \frac{N}{2} -1:
\begin{cases}
x_k = y_k + \omega_N^k z_k \\
x_{k+\frac{N}{2}} = y_k - \omega_N^k z_k
\end{cases}
$$
---
## Observations of the Recursive FFT
* Computational effort $C(N)(N=2^p)$ given by recursion equation$$\Large C(N) = 
\begin{cases}
\mathcal{O}(1) \quad \text{for } \ N=1 \\
\mathcal{O}(N) + 2 C(\frac{N}{2}) \quad \text{for } \ N > 1
\end{cases}
\Rightarrow
C(N) = \mathcal{O}(NlogN)
$$
* Algorithm splits up in 2 phases:
	* resorting of input data
	* combination following the "butterfly scheme"
	> Anticipation of the resorting enabled a simple, iterative algorithm without additional memory requirements.

---
## Sorting Phase of the FFT - Bit Reversal
* even indices are sorted into the upper half, odd indices into the lower half.
* distinction even/odd based on least significan bit
* distinction upper/lower based on most significan bit
> And index in the sorted field has the **reversed** (i.e. mirrored) binary representation compared to the original index. 

---
## Sorting of a Vector (N = 2^p Entries, Bit Reversal)
```C++
/** FFT sorting phase: reorder data in array */
for(int n = 0; n < N; n++){
	// Compute p-bit bit reversal of n in j
	int j = 0; 
	int m = n;
	for(int i = 0; i < p; i++) {
		j = 2*j + m%2; 
		m = m/2;
	}
	// if j>n exchange X[j] and X[n]:
	if(j<n) {
		complex<double> h;
		h = X[j]; 
		X[j] = X[n];
		X[n] = h;
	}
} 
```

Bit reversal needs $\mathcal{O}(p) = \mathcal{O}(NlogN)$ operations
-> Sorting results also in a complexity of $\mathcal{O}(NlogN)$ 
-> Sorting may consume up to 10-30% of the CPU time!

---
# Iterative Implementation of the "Butterflies"
```pseudo

{Loop over the size of the IDFT}
for(int L = 2; L <= N; L*=2)
	{Loop over the IDFT of one level}
	for(int k = 0; k<N; k+=L)
		{perform all butterflies of one level}
		for(int j=0; j<L/2; j++) {
			{complex computation}
			z <-- w^j_l * X[k+j+L/2]
			X[k+j+L/2] <-- X[k+j] - z 
			X[k+j] <-- X[k+j] + z
		}
```
* k-loop are "permutable"!
* How and when ar the $w_L^j$ computed?

### Advantage 
> Suitable for vectorization

> good cache performance due to prefetching (stream access) and usage of cache lines 

### Disadvantage
> multiple computations of $\omega_L^j$ 

