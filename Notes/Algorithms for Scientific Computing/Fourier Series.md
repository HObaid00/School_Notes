# Definition
For a $\Large 2\pi$-periodic function *f*, the corresponding **Fourier series** is defined as 

$$\Large f(x) \sim \sum_{k=-\infty}^{\infty} c_k e^{ikx}$$
where 
$$\Large c_k = \frac{1}{2\pi} \int_0^{2\pi} f(x)e^{-ikx}\,dx$$

The $\Large c_k$ are called (continuous) **Fourier coefficients**.

If *f* is piece-wise smooth, the Fourier series converges point-wise (i.e. for each x) towards

$$\Large
\frac1 2 (f(x^+)+ f(x^-)),
$$
i.e. in particular towards $\Large f(x)$, if *f* is continuously differentiable at x.

---
# Computation of $\Large c_k$ via Midpoint Rule

**Midpoint rule:** evaluate $\Large g(x)$ at midpoints $\Large x_n$:

$$
\Large
\begin{equation}
\int_0^{2\pi} g(x)dx \simeq 
\frac{2\pi}N \sum_{n=0}^{N-1}g(x_n)
\quad \text{with} \quad
x_n := \frac{2 \pi (n+ \frac 1 2)}{N}
\end{equation}
$$

With $\Large g(x) := f(x)e^{-ikx}$ and $\Large f_n := f(x_n)$, we obtain:
$$\Large
c_k \simeq \tilde{F}_k := \frac 1 N \sum_{n=0}^{N-1} f_n e^{-i2\pi (n + \frac 1 2) k/N}
$$
> **"Quarter-Wave Discrete Fourier Transform"**

---
# Links
[[Algorithms for Scientific Computing]]
[[Transformer, signaler och system]]
[[Quarter-Wave DFT]]
[[DFT]]