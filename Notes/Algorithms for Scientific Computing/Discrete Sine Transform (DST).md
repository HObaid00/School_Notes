# Discrete Sine Transform (DST)

The **Discrete Sine Transform (DST)** is a transform closely related to the Discrete Fourier Transform (DFT).  
It is specifically designed for data that has **odd symmetry**.

The DST represents a signal as a weighted sum of sine waves.

---

# Why Sine Functions?

Sine functions naturally satisfy:

$$\Large \sin(-x) = -\sin(x)$$

This means sine functions are **odd functions**.

Therefore, if a data set behaves antisymmetrically around the origin, sine functions provide a natural basis for representing it.

---

# Odd Symmetry

A sequence has odd symmetry if:

$$\Large f_{-n} = -f_n$$

This immediately implies:

$$\Large f_0 = 0$$

because:

$$
f_0 = -f_0 \Rightarrow f_0 = 0
$$

In many DST formulations:

$$\Large f_0 = f_N = 0$$

which corresponds to fixed-zero boundary conditions.

---

# Forward DST

For a sequence:

$$
f_1, f_2, \dots, f_{N-1}
$$

the DST coefficients are:

$$\Large
\hat{F}_k =
\frac{1}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(\frac{\pi nk}{N}\right)
$$

for:

$$
k = 1,2,\dots,N-1
$$

Each coefficient measures how strongly the signal contains a particular sine wave frequency.

---

# Inverse DST

The original signal can be reconstructed using:

$$\Large
f_n =
2
\sum_{k=1}^{N-1}
\hat{F}_k
\sin\left(\frac{\pi nk}{N}\right)
$$

This shows that the DST and inverse DST are inverse operations.

---

# Intuition

The DST decomposes a signal into sine-shaped oscillations.

- Small values of $k$ correspond to low-frequency waves.
- Large values of $k$ correspond to high-frequency oscillations.

The transform tells us how much of each sine pattern appears in the signal.

---

# Example

Suppose:

$$\Large
N=4
$$

and:

$$\Large
f_1 = 1,\quad f_2 = 2,\quad f_3 = 1
$$

Then the first DST coefficient is:

$$\Large
\hat{F}_1 =
\frac{1}{4}
\left[
1\sin\left(\frac{\pi}{4}\right)
+
2\sin\left(\frac{2\pi}{4}\right)
+
1\sin\left(\frac{3\pi}{4}\right)
\right]
$$

Using:

$$\Large
\sin\left(\frac{\pi}{4}\right)=\frac{\sqrt2}{2}
$$

and:

$$\Large
\sin\left(\frac{\pi}{2}\right)=1
$$

we obtain:

$$\Large
\hat{F}_1
=
\frac14
\left(
\frac{\sqrt2}{2}
+2+
\frac{\sqrt2}{2}
\right)
$$

This coefficient measures the strength of the lowest sine frequency in the signal.

---

# Applications

The DST is widely used in:

- Solving partial differential equations
- Heat equation simulations
- Image processing
- Signal processing
- Scientific computing

It is especially useful when the boundaries are fixed to zero.

---

# Key Idea

The DST is essentially a DFT applied to data extended with odd symmetry.

This connection allows the DST to be computed efficiently using FFT algorithms.

----
# Links
[[Algorithms for Scientific Computing]]
