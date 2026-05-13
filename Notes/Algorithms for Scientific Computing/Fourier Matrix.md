# Definition
* W is symmetric: W = W^T, and has the form:
$$\Large
W = 
\begin{pmatrix}
\omega_N^0 & \omega_N^0 & \omega_N^0 & \dots & \omega_N^0 \\
\omega_N^0 & \omega_N^1 & \omega_N^2 & \dots & \omega_N^{(N-1)} \\
\omega_N^0 & \omega_N^2 & \omega_N^4 & \dots & \omega_N^{2(N-1)} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
\omega_N^0 & \omega_N^{(N-1)} & \omega_N^{(2N-1)} & \dots & \omega_N^{(N-1)(N-1)} \\

\end{pmatrix}
$$
### Orthogonality relation
$$\Large
W (W^T)^* = WW^H = N I 
$$
since 
$$
\Large
[WW^H]_{kl} = \sum_{j=0}^{N-1} \omega_N^{kj}(\omega_N^{ij})^* = \sum_{j=0}^{N-1} \omega_N^{(k-l)j} = 
\begin{cases}
N \ \text{if } k = l \\
0 \ \text{if } \not= l
\end{cases}
$$
> inverse of W easily available!

---
# Inverse
Since $$\Large WW^H = NI$$
the inverse of 
$$\Large
W^{-1} = \frac{1}{N}
\begin{pmatrix}
\omega_N^0 & \omega_N^0 & \omega_N^0 & \dots & \omega_N^0 \\
\omega_N^0 & \omega_N^-1 & \omega_N^-2 & \dots & \omega_N^{-(N-1)} \\
\omega_N^0 & \omega_N^-2 & \omega_N^-4 & \dots & \omega_N^{-2(N-1)} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
\omega_N^0 & \omega_N^{-(N-1)} & \omega_N^{-(2N-1)} & \dots & \omega_N^{-(N-1)(N-1)} \\
\end{pmatrix}
$$

---
# Compute Fourier Coefficients 
The vector $F$ of the Fourier coefficients can be computed easily as a matrix-vector product - with computational effort $\mathcal{O}(N^2)$: 
$$\Large
F = \frac{1}{N} W^H f  \ \text{ or } \ F_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n \omega_N ^{-nk}
$$

---
# (EXTRA) Properties of the Fourier Matrix $W$ (details)

- **Important property #1:**
$$\Large
(\omega_N^k)^N = e^{N \cdot i 2\pi k / N} = e^{i2\pi k} = 1
$$

- **Important property #2:**
$$\Large
(\omega_N^k)^* = \left(e^{i2\pi k/N}\right)^*
= \left(\cos\left(\frac{2\pi k}{N}\right) + i \sin\left(\frac{2\pi k}{N}\right)\right)^*
$$
$$\Large
= \cos\left(\frac{2\pi k}{N}\right) - i \sin\left(\frac{2\pi k}{N}\right)
= \cos\left(-\frac{2\pi k}{N}\right) + i \sin\left(-\frac{2\pi k}{N}\right)
= e^{-i2\pi k/N} = \omega_N^{-k}
$$

- **Orthogonality relation:**
$$\Large
W (W^T)^* = W W^H = N I
$$

Since:
$$\Large
[W W^H]_{kl}
= \sum_{j=0}^{N-1} \omega_N^{kj} \left(\omega_N^{lj}\right)^*
= \sum_{j=0}^{N-1} \omega_N^{kj} \omega_N^{-lj}
= \sum_{j=0}^{N-1} \omega_N^{(k-l)j}
$$

---

- **Case 1: $k = l$**
$$ \Large
\sum_{j=0}^{N-1} \omega_N^{(k-l)j}
= \sum_{j=0}^{N-1} \omega_N^0
= \sum_{j=0}^{N-1} 1
= N
$$

---

- **Case 2: $k \ne l$**

Let:
$$\Large
\xi = \omega_N^{(k-l)}
$$

Then:
$$\Large
\sum_{j=0}^{N-1} \omega_N^{(k-l)j}
= \sum_{j=0}^{N-1} \xi^j
$$

Using geometric series:
$$\Large
(1 - \xi)\sum_{j=0}^{N-1} \xi^j
= \sum_{j=0}^{N-1} \xi^j - \sum_{j=0}^{N-1} \xi^{j+1}
= 1 - \xi^N
$$

Thus:
$$\Large
\sum_{j=0}^{N-1} \xi^j = \frac{1 - \xi^N}{1 - \xi}
$$

Since:
$$\Large
(\omega_N^k)^N = 1
$$

we get:
$$\Large
\xi^N = 1
\quad \Rightarrow \quad
\sum_{j=0}^{N-1} \omega_N^{(k-l)j} = 0
$$

---

- **Conclusion (orthogonality):**
$$\Large
\sum_{j=0}^{N-1} \omega_N^{(k-l)j}
=
\begin{cases}
N, & k = l \\
0, & k \ne l
\end{cases}
$$
