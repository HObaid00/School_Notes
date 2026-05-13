# Fast Fourier Transform for N=2^p 

### Basic Idea:
Seperate polynomials by their even and odd counterparts **(Divide-and-Conquer)**

sum up even and odd indices separately in IDFT
-> first for n = 0, 1, .., $\frac{N}{2} -1$:
$$\Large
x_n = \sum_{k=0}^{N-1}X_k \omega_N^{nk} =
\sum_{k=0}^{\frac{N}{2}-1}X_{2k} \omega_N^{2nk} + 
\sum_{k=0}^{\frac{N}{2}-1}X_{2k+1} \omega_N^{(2k+1)n} 
$$
We set 
$$\Large 
Y_k := X_{2k}
$$
and 
$$\Large
Z_k := X_{2k+1}
$$
use 
$$\Large
\omega_N ^{2nk} = \omega_{N/2}^{nk}
$$
and get a sum of two IDFT on $N/2$ coefficients:
$$
\Large
x_n = \sum_{k=0}^{N-1}X_k \omega_N^{nk} =
\sum_{k=0}^{\frac{N}{2}-1}
Y_{k} \omega_{N/2}^{nk} + 

\omega_N^n
\sum_{k=0}^{\frac{N}{2}-1}
Z_k \omega_{N/2}^{nk} 

$$
where
$$\Large
\sum_{k=0}^{\frac{N}{2}-1}
Y_{k} \omega_{N/2}^{nk} 
:= y_n, 
\quad

\sum_{k=0}^{\frac{N}{2}-1}
Z_k \omega_{N/2}^{nk} := z_n
$$
Note: this fomula is actually valid for all $n = 0, \dots , N-1$, however, the IDFTs of size $N/2$ will only feliver the $y_n$ and $z_n$ for $n=0,\dots, \frac{N}{2} - 1$ (but: $\Large y_n, \ z_n$ are periodic!) 

---
# Sorting Phase of the FFT - Bit Reversal

# FFT function in Pseudo Code
![[Pasted image 20260421143225.png]]