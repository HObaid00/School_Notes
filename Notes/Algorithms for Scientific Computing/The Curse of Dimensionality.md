# The Curse of Dimensionality

Many algorithms become exponentially harder in higher dimensions.

This phenomenon is called the curse of dimensionality.

---

# Grid Growth

Suppose:

- each dimension uses $n$ grid points
- the space has dimension $d$

Then the total number of grid points becomes:

$$\Large
n^d
$$

---

# Example

If:

$$
n=100
$$

then:

| Dimensions | Grid Points |
|---|---|
| 1D | $100$ |
| 2D | $10^4$ |
| 3D | $10^6$ |
| 10D | $10^{20}$ |

The growth becomes catastrophic.

---

# Why This is a Problem

High-dimensional problems require:

- huge memory
- enormous computation time
- massive training data

---

# Real-World Example

Handwritten digit recognition may use:

$$\Large
64
$$

dimensions.

A naive full grid becomes impossible.

---

# Sparse Grids

Sparse grids reduce complexity by:

- ignoring unimportant basis functions
- combining only important hierarchical components

---

# Main Idea

Many high-dimensional functions contain structure.

Sparse grids exploit this structure to avoid exponential growth.

----
# Links
[[Algorithms for Scientific Computing]]