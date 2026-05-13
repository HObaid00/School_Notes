## DFT and Symmetry

### Input Transform Types
- Real input → **Real DFT (RDFT)**
- Even symmetry: $f_n = f_{-n}$ → **DCT**
- Odd symmetry: $f_n = -f_{-n}$ → **DST**

### Quarter-Wave Transforms
- Even: $f_n = f_{-n-1}$ → QW-DCT  
- Odd: $f_n = -f_{-n-1}$ → QW-DST  

---

## Real-Valued DFT (RDFT)

Assume real input $f_n \in \mathbb{R}$:

$$\Large
F_k = \frac{1}{N} \sum f_n \left( \cos\left(\frac{2\pi nk}{N}\right) - i \sin\left(\frac{2\pi nk}{N}\right) \right)
$$

### Properties
Real part:
$$\Large
\mathrm{Re}(F_k) = \frac{1}{N} \sum f_n \cos\left(\frac{2\pi nk}{N}\right)
$$

Imaginary part:
$$\Large
\mathrm{Im}(F_k) = -\frac{1}{N} \sum f_n \sin\left(\frac{2\pi nk}{N}\right)
$$

Symmetry:
$$\Large
F_k^* = F_{-k}
$$

➡️ Only $N$ independent real coefficients are needed.

---

## Real DFT Representation

Mapping:

$$\Large
(f_{-N/2+1}, \dots, f_0, \dots, f_{N/2})
$$

$$\Large
\Downarrow \text{DFT / IDFT} \Uparrow
$$

$$\Large
(F_0, \mathrm{Re}(F_1), \mathrm{Im}(F_1), \dots, \mathrm{Re}(F_{N/2-1}), \mathrm{Im}(F_{N/2-1}), F_{N/2})
$$

---

## Goal of RDFT

- Input: $N$ real values  
- Output: $N$ real coefficients  

Using symmetry:
$$\Large
F_{-k} = F_k^*
$$

---

## RDFT Formulation

$$\Large
\mathrm{Re}(F_k) = \frac{1}{N} \sum f_n \cos\left(\frac{2\pi nk}{N}\right)
$$

$$\Large
\mathrm{Im}(F_k) = -\frac{1}{N} \sum f_n \sin\left(\frac{2\pi nk}{N}\right)
$$

---

## Inverse Real DFT

$$\Large
f_n = F_0 + 2 \sum_{k=1}^{N-1} \left( \mathrm{Re}(F_k)\cos\left(\frac{\pi nk}{N}\right) - \mathrm{Im}(F_k)\sin\left(\frac{\pi nk}{N}\right) \right) + F_N \cos(\pi n)
$$

Define:
- $a_k = 2\mathrm{Re}(F_k)$  
- $b_k = -2\mathrm{Im}(F_k)$  

Then:

$$\Large
f_n = a_0 + \sum_{k=1}^{N-1} \left( a_k \cos\left(\frac{\pi nk}{N}\right) + b_k \sin\left(\frac{\pi nk}{N}\right) \right) + a_N \cos(\pi n)
$$

---

## Alternative (Textbook) Form

$$\Large
f_n = \frac{1}{2}a_0 + \sum_{k=1}^{N-1} \left( a_k \cos\left(\frac{\pi nk}{N}\right) + b_k \sin\left(\frac{\pi nk}{N}\right) \right) + \frac{1}{2}a_N \cos(\pi n)
$$

---

## Trigonometric Interpolation Interpretation

Basis functions:
- $\cos(kx)$ for $k = 0,\dots,N$
- $\sin(kx)$ for $k = 1,\dots,N-1$

Grid points:
$$\Large
x_n = \frac{\pi n}{N}, \quad n = -N+1,\dots,N
$$

➡️ RDFT corresponds to interpolation in a trigonometric basis.

---

## Fast Real DFT

Naive FFT is inefficient for real data:
- Redundant symmetric components  
- Unnecessary complex arithmetic  

### Improvements
1. Two real DFTs from one complex FFT  
2. Real DFT (size $2N$) from complex FFT (size $N$)  
3. Compact real FFT using symmetry  

---

## Two Real DFTs from One FFT

Let:
$$\Large
f_n = g_n + i h_n
$$

Then:
$$\Large
F_k = G_k + iH_k
$$

Recover:
$$\Large
G_k = \frac{1}{2}(F_k + F_{-k}^*)
$$

$$\Large
H_k = -\frac{i}{2}(F_k - F_{-k}^*)
$$

### Algorithm
```text
1. f_n = g_n + i h_n
2. Compute FFT → F_k
3. Extract G_k, H_k
   