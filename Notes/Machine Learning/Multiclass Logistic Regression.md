# Multiclass Logistic Regression

Binary logistic regression uses sigmoid.

Multiclass logistic regression uses softmax.

---

# Model

For class $c$:

$$\Large
p(y=c|x)
=
\frac{
e^{w_c^Tx}
}{
\sum_{c'} e^{w_{c'}^Tx}
}
$$

---

# Interpretation

Each class gets a score:

$$
w_c^Tx
$$

Softmax converts scores into probabilities.

---

# One-Hot Encoding

Labels are represented as vectors:

$$
(0,0,1,0)
$$

meaning:

- sample belongs to class 3

---

# Cross Entropy Loss

The loss becomes:

$$\Large
E(w)
=
-\sum_{i=1}^{N}
\sum_{c=1}^{C}
y_{ic}\log p(y_i=c|x_i,w)
$$

---

# Importance

This is one of the most important loss functions in modern deep learning.

---
# Links
[[Machine Learning]]