# Softmax Function

Softmax generalizes the sigmoid function to multiple classes.

---

# Definition

For a vector:

$$
x=(x_1,\dots,x_K)
$$

softmax is:

$$\Large
\sigma(x)_i
=
\frac{
e^{x_i}
}{
\sum_{k=1}^{K} e^{x_k}
}
$$

---

# Properties

Each output satisfies:

$$
0 \le \sigma(x)_i \le 1
$$

and:

$$
\sum_i \sigma(x)_i=1
$$

Thus outputs form a valid probability distribution.

---

# Interpretation

The largest score gets the largest probability.

---

# Example

Input scores:

$$
(2,1,0)
$$

might produce:

$$
(0.67,0.24,0.09)
$$

---

# Usage

Softmax is widely used in:

- multiclass logistic regression
- neural networks
- language models

---
# Links
[[Machine Learning]]
