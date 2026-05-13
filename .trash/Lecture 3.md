
## DFT as Matrix–Vector Product

$$\Large
F_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n \omega_N^{-nk}, \quad
f_n = \sum_{k=0}^{N-1} F_k \omega_N^{nk}
$$

Matrix form:
$$\Large
F = \frac{1}{N} W^H f, \quad f = W F
$$

- Complexity: $O(N^2)$  
- Goal: reduce complexity  

---

## FFT Idea

Use **divide-and-conquer**:

- Split into even and odd indices
- Compute two smaller transforms

---

## Splitting the Sum

$$\Large
x_n = \sum_{k=0}^{N-1} X_k \omega_N^{nk}
$$

Split:

$$\Large
x_n =
\sum_{k=0}^{N/2-1} X_{2k} \omega_N^{2nk}
+
\sum_{k=0}^{N/2-1} X_{2k+1} \omega_N^{(2k+1)n}
$$

Define:
- $Y_k = X_{2k}$
- $Z_k = X_{2k+1}$

Then:

$$\Large
x_n = y_n + \omega_N^n z_n
$$

---

## Butterfly Scheme

$$\Large
x_k = y_k + \omega_N^k z_k
$$

$$\Large
x_{k+N/2} = y_k - \omega_N^k z_k
$$

- Core building block of FFT
- Combines two smaller FFTs

---

## Recursive FFT Algorithm

```text
rekFFT(X):
1. Split:
   Y_n = X_{2n}
   Z_n = X_{2n+1}

2. Recursive calls:
   y = rekFFT(Y)
   z = rekFFT(Z)

3. Combine:
   for k = 0,...,N/2-1:
       x[k]       = y[k] + ω_N^k * z[k]
       x[k+N/2]   = y[k] - ω_N^k * z[k]