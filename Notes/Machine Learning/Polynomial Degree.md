# Overfitting and Polynomial Degree

Choosing model complexity is extremely important.

---

# Polynomial Degree

Higher polynomial degree means more flexible models.

Examples:

| Degree | Behavior |
|---|---|
| $M=0$ | constant |
| $M=1$ | straight line |
| $M=3$ | smooth nonlinear curve |
| $M=9$ | highly flexible |

---

# Underfitting

If the model is too simple:

- important structure is missed
- predictions are poor

This is called:

$$\Large
\text{underfitting}
$$

---

# Overfitting

If the model is too flexible:

- it memorizes noise
- generalization becomes poor

This is called:

$$\Large
\text{overfitting}
$$

---

# Observation from the Lecture

High-degree polynomials often produce huge coefficients:

$$
|w_j|\gg1
$$

This creates unstable oscillations.

![[Pasted image 20260506193216.png]]

---

# Train vs Validation Error

Typically:

- training error decreases with complexity
- validation error eventually increases

Good models minimize validation error, not training error.

---
# Links
[[Machine Learning]]
