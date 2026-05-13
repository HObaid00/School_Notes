
# Problem 
Naive FFT is inefficient for real data:
- Redundant symmetric components  
- Unnecessary complex arithmetic  

### Improvements
1. Two real DFTs from one complex FFT  
2. Real DFT (size $2N$) from complex FFT (size $N$)  
3. Compact real FFT using symmetry  

---
# Two Real DFTs from One FFT

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
---
## Algorithm
```text
1. f_n = g_n + i h_n
2. Compute FFT → F_k
3. Extract G_k, H_k
   