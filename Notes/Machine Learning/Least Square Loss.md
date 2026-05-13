# Least Squares Loss

To find the best model, we must measure prediction error.

The standard choice is the least squares loss.

---

# Prediction Error

For one sample:

$$\Large
f_w(x_i)-y_i
$$

measures the difference between:

- predicted value
- true value

![[Pasted image 20260503131613.png|682]]


---

# Least Squares Objective

The total error is:

$$\Large
E_{LS}(w)
=
\frac12
\sum_{i=1}^{N}
(f_w(x_i)-y_i)^2
$$

or:

$$\Large
E_{LS}(w)
=
\frac12
\sum_{i=1}^{N}
(w^Tx_i-y_i)^2
$$

---

# Why Squared Errors?

Squaring has important advantages:

- positive and negative errors do not cancel
- large errors are penalized strongly
- optimization becomes mathematically convenient

---

# Matrix Form

Using:

$$
X=
\begin{bmatrix}
x_1^T\\
x_2^T\\
\vdots\\
x_N^T
\end{bmatrix}
$$

the loss becomes:

$$\Large
E_{LS}(w)
=
\frac12
(Xw-y)^T(Xw-y)
$$

---

# Goal

Find:

$$\Large
w^*
=
\arg\min_w E_{LS}(w)
$$

the weights minimizing prediction error.

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
[[Moore-Penrose Pseudo Inverse]]
[[Gradient]]
