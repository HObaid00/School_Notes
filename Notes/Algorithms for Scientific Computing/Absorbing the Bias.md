# Bias Term

Linear regression often includes a bias term:

$$\Large
f_w(x)=w_0+w^Tx
$$

where:

- $w_0$ shifts the prediction upward or downward

---

# Absorbing the Bias

To simplify notation, we augment the feature vector:

$$\Large
\tilde{x}=
(1,x_1,\dots,x_D)^T
$$

and the weight vector:

$$\Large
\tilde{w}=
(w_0,w_1,\dots,w_D)^T
$$

Then:

$$\Large
f_w(x)=\tilde{w}^T\tilde{x}
$$

---

# Why This is Useful

Now the bias becomes just another weight.

This allows all formulas to use compact matrix notation.

---

# Example

Suppose:

$$
w_0=3,\quad w_1=2
$$

and:

$$
x=5
$$

Then:

$$
f(x)=3+2\cdot5=13
$$

Using augmented vectors:

$$
\tilde{x}=(1,5)
$$

$$
\tilde{w}=(3,2)
$$

and:

$$
\tilde{w}^T\tilde{x}=13
$$

Same result, simpler notation.

---
# Links
[[Machine Learning]]