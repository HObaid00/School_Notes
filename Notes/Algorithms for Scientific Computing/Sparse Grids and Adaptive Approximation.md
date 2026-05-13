# Sparse Grids and Adaptive Approximation

Sparse grids are designed to fight the curse of dimensionality.

They use only the most important basis functions.

---

# Adaptive Refinement

Instead of refining everywhere equally:

- refine where the function changes rapidly
- keep coarse representation elsewhere

---

# Hierarchical Surplus

Each basis function contributes some amount to the approximation.

Small contributions can often be ignored.

Large contributions indicate important features.

---

# Sparse Grid Philosophy

Keep only basis functions with significant impact.

This dramatically reduces complexity.

---

# Example: Classification Boundary

The lecture shows adaptive sparse-grid classification on the Ripley data set.

The algorithm automatically places more basis functions near complicated boundaries.

---

# Benefits

Sparse grids can achieve:

- high accuracy
- reduced memory usage
- faster computations

especially in moderately high dimensions.

---

# Applications

Sparse grids are used in:

- machine learning
- uncertainty quantification
- PDE solvers
- finance
- scientific computing

---

# Key Insight

Most high-dimensional problems contain local structure.

Sparse grids exploit this structure efficiently.

---
[[Sparse Grids]]
[[Algorithms for Scientific Computing]]
