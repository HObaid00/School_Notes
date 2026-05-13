
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
