# Spectral Methods

Spectral methods solve problems in the **frequency domain** instead of directly in physical space.

The key idea is:

1. Transform the problem into frequencies.
2. Solve it more easily there.
3. Transform the solution back.

![[Pasted image 20260506121602.png]]

---

# Space Domain vs Frequency Domain

In the space domain, we work directly with values like:

- temperatures
- sound amplitudes
- image pixels

In the frequency domain, we describe the same data using:

- sine waves
- cosine waves
- oscillation frequencies

---

# Why Transform the Problem?

Many equations become simpler in frequency space.

Complicated differential operators become simple multiplications.

For example:

$$\Large
\frac{d^2}{dx^2}\sin(kx)
=
-k^2\sin(kx)
$$

Differentiation becomes multiplication by:

$$
-k^2
$$

This is much easier computationally.

---

# Main Workflow

The standard spectral-method workflow is:

$$
\text{Problem}
\rightarrow
\text{Transform}
\rightarrow
\text{Solve}
\rightarrow
\text{Inverse Transform}
$$

Common transforms include:

- FFT
- DCT
- DST

---

# Examples of Spectral Methods

## 1. Fast Poisson Solvers

Transforms convert PDEs into simpler algebraic equations.

---

## 2. JPEG Compression

Images are transformed into frequency coefficients.

Small coefficients are discarded to save space.

---

## 3. Signal Filtering

High frequencies can be removed to reduce noise.

Low frequencies can be removed to sharpen edges.

---

# Intuition

A complicated signal can be viewed as a combination of simple waves.

Spectral methods solve the problem wave-by-wave.

---
# Links
[[Algorithms for Scientific Computing]]