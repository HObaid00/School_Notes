# Definition

$$\Large c_k \approx \frac{1}{N} \left(\frac{f_0}{2} + \sum_{n=1}^{N-1} f_n e^{-i2\pi nk/N} + \frac{f_N}{2}\right)$$

For periodic data: if $\Large f_0 = f_N$ (periodic data), we obtain

$$\Large c_k \simeq F_k = \frac{1}{N}\sum_{n=0}^{N-1} f_n e^{-i2\pi nk/N}$$
* $\Large F_k$ are approximations of $\Large c_k$
* approximate computation leads to solution of the interpolation problem
* approximation error is of order $\Large \mathcal{O}(N^{-2})$ 

For $\Large f_0 \not= f_N$, or for "discontinuities", we get a recommendation:

> **Average Values at Endpoints and Discontinuities (AVED)**

---
# Links
[[Algorithms for Scientific Computing]]
