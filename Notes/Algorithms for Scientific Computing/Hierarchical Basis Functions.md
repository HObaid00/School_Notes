# Hierarchical Basis Functions

Hierarchical basis functions use multiple resolution levels simultaneously.

They combine:

- coarse global functions
- fine local corrections

---

# Motivation

A single grid resolution is often insufficient.

We want:

- coarse functions for smooth regions
- fine functions for detailed regions

---

# Mother Hat Function

The fundamental basis function is:

$$\Large
\phi(x)=\max(1-|x|,0)
$$

This is a triangular hat centered at zero.

---

# Scaled and Shifted Functions

Basis functions on level $n$ are:

$$\Large
\phi_{n,i}(x)
=
\phi\left(
\frac{x-x_{n,i}}{h_n}
\right)
$$

where:

$$
h_n=2^{-n}
$$

and:

$$
x_{n,i}=ih_n
$$

---

# Hierarchical Construction

The hierarchical basis uses only odd-indexed nodes on each level.

This avoids redundancy between coarse and fine levels.

---

# Main Idea

The approximation becomes:

$$
\text{coarse approximation}
+
\text{fine corrections}
$$

---

# Why This Helps

Hierarchical bases:

- adapt naturally to local complexity
- reduce overfitting
- support adaptive refinement
- are important for sparse grids

---

# Key Insight

Fine-scale functions only correct details missed by coarser levels.

---
# Links
[[Interpolation and Basis Functions]]
[[Algorithms for Scientific Computing]]