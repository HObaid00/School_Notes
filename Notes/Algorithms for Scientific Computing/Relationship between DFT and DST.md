# Relationship Between DFT and DST

The DST can be derived from the Discrete Fourier Transform (DFT).

The key idea is to extend the data using **odd symmetry** and then apply the DFT.

---

# Discrete Fourier Transform (DFT)

The DFT of a sequence $f_n$ is:

$$\Large
F_k =
\frac{1}{N}
\sum_{n=0}^{N-1}
f_n
e^{-2\pi i nk/N}
$$

The exponential term contains both cosine and sine parts:

$$
e^{-ix} = \cos(x) - i\sin(x)
$$

---

# Effect of Odd Symmetry

Suppose the signal satisfies:

$$\Large
f_{-n} = -f_n
$$

Then cosine terms cancel out because cosine is even:

$$
\cos(-x)=\cos(x)
$$

while sine terms survive because sine is odd:

$$
\sin(-x)=-\sin(x)
$$

As a result, the DFT simplifies into a pure sine expansion.

---

# Resulting Formula

After simplification:

$$\Large
F_k =
-\frac{i}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(\frac{\pi nk}{N}\right)
$$

The transform coefficients are purely imaginary.

Removing the factor $-i$ gives the standard DST definition.

---

# Why This Matters

This derivation is important because it means:

1. The DST inherits properties of the DFT.
2. The DST can be computed using FFT algorithms.
3. Fast computation reduces complexity from:

$$
O(N^2)
$$

to:

$$
O(N\log N)
$$

which is dramatically faster for large signals.

---

# Conceptual Picture

The workflow is:

1. Extend the signal with odd symmetry.
2. Apply the FFT.
3. Extract the sine-related components.

This is how fast DST implementations work internally.

---
# Links
[[Algorithms for Scientific Computing]]