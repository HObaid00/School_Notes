# Fast Poisson Solver Algorithm

The fast Poisson solver uses the Fast Sine Transform (FST).

---

# Step 1 — Transform the Right-Hand Side

Compute:

$$\Large
F_k
=
\frac{1}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(\frac{\pi nk}{N}\right)
$$

using the Fast Sine Transform.

---

# Step 2 — Solve in Frequency Space

Compute:

$$\Large
U_k
=
\frac{F_k}
{
2-2\cos\left(\frac{\pi k}{N}\right)
}
$$

This is inexpensive because each coefficient is independent.

---

# Step 3 — Transform Back

Recover the solution:

$$\Large
u_n
=
2
\sum_{k=1}^{N-1}
U_k
\sin\left(\frac{\pi nk}{N}\right)
$$

using the inverse Fast Sine Transform.

---

# Computational Complexity

The two transforms require:

$$\Large
O(N\log N)
$$

operations.

The middle step requires:

$$\Large
O(N)
$$

operations.

Total complexity:

$$\Large
O(N\log N)
$$

---

# Why This Matters

For very large 2D and 3D problems:

- direct solvers become too expensive
- FFT-based methods remain practical

This makes spectral Poisson solvers extremely important in scientific computing.

---

# Conditions for Using the Method

The algorithm assumes:

1. rectangular domains
2. Cartesian grids
3. constant material parameters
4. zero boundary conditions

Different geometries require other numerical methods.

---
# Links
[[Algorithms for Scientific Computing]]