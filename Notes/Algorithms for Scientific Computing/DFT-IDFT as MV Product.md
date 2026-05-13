# The Pair DFT/IDFT as Matrix Vector Product
Wit the notation 
$$
\Large\omega_N := e^{i2\pi/N} ,
$$
i.e
$$\Large
\omega_N^{-nk} := e^{-i2\pi nk/N}
$$
we formulate the DFT/IDFT as
$$\Large
F_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n\omega_N^{-nk} \quad f_n = \sum_{k=0}^{N-1} F_k \omega_N^{nk}
$$
With the vectors $f:= (f_0, \dots, f_{N-1})$ and $F := (F_0, \dots, F_{N-1})^T$, we denote (and compute) the DFT and IDFT as matrix-vector products
$$\Large
F = \frac{1}{N} W^Hf \qquad f= WF,
$$
where the elements of the Fourier matrix W are $W_{nk} := \omega_N^{nk}$. 

with a **computational complexity of $O(N^2)$. 

Note that
$$\Large
DFT(f) = \frac{1}{N}\bar{IDFT(\bar{f})}
$$
A fast computation is possible via the **divide-and-conquer** approach.
