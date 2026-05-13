
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

>Only $N$ independent real coefficients are needed.

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
