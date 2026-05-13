# Definition

Forward:

$$\Large \tilde{F}_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)$$

Inverse:

$$\Large f_n = \tilde{F}_0 + 2 \sum_{k=1}^{N-1} \tilde{F}_k \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)$$

---
# Properties

- Real-valued transform  
- Works for non-periodic data  
- Efficient via FFT: $\Large O(N \log N)$  

---
# Explanation

When the [[Quarter-Wave DFT]] is symmetric it follows the cosine function.

The standard DFT implicitly assumes **periodic boundary conditions**. That is fine when the function is cyclic or naturally periodic. 

Many setups or functions, especially on finite line segments or grids have **reflective or fixed boundaries**, not periodic ones. The DCT correspond to an  **even extension** of the signal, which effectively models reflective boundaries.

So the motivation is:
* **QW-DFT -> periodic domain (wrap-around behaviour)
* **QW-DCT -> reflective boundaries (more realistic for finite domains)**

---
# QW-DCT Algorithm
**Reduce to Real FFT:**

#### (1) for n = 0, ..., *N*-1:
$$\Large
g_n = f_n \quad g_{2N-n-1} = f_n
$$
#### (2) 2*N*-Real-FFT: compute $G_k$ from $\Large g_n$ (for k = 0, ..., N)
#### (3) for k = 0, ..., *N*-1:
$$\Large
\tilde{F}_k = G_k e^{-i\pi k / 2N}
$$

#### Important Note:
* this results in an algorithm that requires $\mathcal{O}(N\log N)$ operations (FFT!)
* whereas computing all $$\Large \tilde{F}_k = \frac 1 2 \sum f_n \cos \left(\pi k (n + \frac 1 2) / N \right)$$ would require $\Large \mathcal{O}(N^2)$ operations

#### Possible Further Optimissations:
* substitute real 2N-FFT by complex N-FFT
* compact (divide-and-conquer) real FFT
* see Compact Fast QW-DCT 

---
# Compact Fast QW-DCT (Swarztrauber, 1986)

#### QW-DCT with symmetry $\Large f_{2N-n-1} = f_n$
$$\Large
\tilde{F}_k \frac 1 {2N}  \sum_{n=0}^{2N-1} f_n \omega_{2N}^{-k(nt \frac 1 2)} \longrightarrow
\tilde{F}_k \frac 1 {2N}  \sum_{n=0}^{2N-1} f_n \cos \left( \frac{\pi k (n + \frac 1 2)} N \right) 

$$

#### Split into even and odd indices: $\Large g_n := f_{2n}$ and $\Large h_n := f_{2n+1}$ (as in FFT)
* $\Large g_n := f_{2n}$: $$\Large g_n = f_{2n} = f_{2N-n-1} = f_{2(N-n)-1} = f:_{2(N-n-1)+1} = h_{N-n-1} $$
* $\Large h_n := f_{2n+1}$: $$\Large h_n= f_{2n+1} = f_{2N - (2n+1) -1} = f_{2(N-n-1)} = g_{N-n-1} $$
* thus: **two real DFTs** with symmetric data sets see exercises: revered-data DFT easily obtained from DFT 

#### Consider backwards transform: 
with symmetry $\Large \tilde{F}_{2N-k} = - \tilde{F}_k$
$$\Large
f_n := \sum_{k=0}^{2N-1} \tilde{F}_k e^{i2\pi (n + \frac{1}2) k /2N}
\longrightarrow
f_n = \tilde{F}_0 + 2 \sum_{k=1}^{N-1} \tilde {F}_k \cos \left(\frac{\pi k (n + \frac 1 2 } N\right)
$$

#### Split into even and odd indices: (as in FFT)
* $\Large G_k := \tilde{F}_{2k}$: **again leads to Inverse QW-DCT $$\Large -G_k = -\tilde{F}_{2k} = \tilde{F}_{2N-2k} = \tilde{F}_{2(N-k)} = G_{N-k} $$
* $\Large H_k := \tilde{F}_{2k+1}$: **leads to new kind of inverse DCT** $$\Large -H_k = -\tilde{F}_{2k+1} = \tilde{F}_{2N-(2k+1)} = \tilde{F}_{2(N-k)-1} = \tilde{F}_{2(N-k-1)+1} = H_{N-k-1}  $$
>(next even/odd split leads to two real DFTs with symmetric data sets)

---
# Links

[[Algorithms for Scientific Computing]]