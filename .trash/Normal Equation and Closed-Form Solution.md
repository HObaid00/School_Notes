# Normal Equation and Closed-Form Solution

Linear regression has a closed-form mathematical solution.

---

# Gradient of the Loss

Starting from:

$$\Large
E_{LS}(w)
=
\frac12
(Xw-y)^T(Xw-y)
$$

the gradient is:

$$\Large
\nabla_w E_{LS}(w)
=
X^TXw-X^Ty
$$

---

# Optimality Condition

At the minimum:

$$\Large
\nabla_w E_{LS}(w)=0
$$

Therefore:

$$\Large
X^TXw=X^Ty
$$

This is called the **normal equation**.

---

# Closed-Form Solution

Solving for $w$ gives:

$$\Large
w^*
=
(X^TX)^{-1}X^Ty
$$

---

# Pseudoinverse

The expression:

$$\Large
X^\dagger=(X^TX)^{-1}X^T
$$

is called the Moore–Penrose pseudoinverse.

Then:

$$\Large
w^*=X^\dagger y
$$

---

# Why This Matters

Unlike many machine learning methods, linear regression can often be solved directly without iterative optimization.

---
# Links
[[Machine Learning]]
[[Minsta Kvadrat Metoden (MK)]]