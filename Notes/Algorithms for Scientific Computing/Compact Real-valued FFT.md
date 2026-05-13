Compute DFT of a real valued vector $(f_{-N +1}, \dots, f_N)$:
$$\Large
F_k = \frac{1}{2N} \sum_{-N+1}^N f_n\omega_{2N}^{-nk} \quad \text{for} \quad k = 0, \dots, N
$$
Split up in $g_n := f_{2n}$ and $h_n := f_{2n-1}$; leads to butterfly scheme:
$$\Large
F_k = \frac{1}{2} (G_k + \omega_{2n}^kH_k) \quad \text{for } \ k = 0, \dots, N
$$
$$\Large
F_{k+N} = \frac{1}{2} (G_k - \omega_{2n}^kH_k) \quad \text{for } \ -\frac{N}{2} +1, \dots, 0 
$$
$G_k$ and $H_k$ are coefficients of a real-valued DFT of length *N*; hence:
$$\Large
G_k = G_{-k}^* \quad \text{and}\quad H_k = H_{-k}^* \quad \text{for } \ k = 0, \dots, \frac{N}{2} -1
$$

Use symmetry of $G_k$ and $H_k$ for the computation of $F_k$: 
$$\Large
F_k \frac 1 2 (G_k \omega_{2N}^k H_k) \quad \text{for } \ k = 0, \dots, \frac N 2 
$$
$$\Large
F_{N-k} = \frac{1}{2} 
(G_{-k} - \omega_{2N}^{-k} H_{-k})  =  
\frac{1}{2}
(G_k - \omega_{2N}^{k} H_{k})^*

$$
$$\Large
\text{for } \ k = 0, \dots, \frac{N}{2} -1
$$
> Computation of $F_k$ (for k = 0, ..., N) reduced to the computation of $G_k$ and $H_k$ 
> (for k = 0, ..., N/2, respectively) 

