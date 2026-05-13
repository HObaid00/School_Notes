# Nonlinear Regression with Basis Functions

Real-world relationships are often nonlinear.

Example:

$$
y=\sin(2\pi x)
$$

A straight line cannot model this well.

---

# Key Idea

Transform the input using basis functions.

Instead of:

$$
f(x)=w_0+w_1x
$$

use:

$$\Large
f(x)
=
w_0+
\sum_{j=1}^{M}
w_j\phi_j(x)
$$

---

# Important Insight

The model may be nonlinear in $x$ but remains linear in the weights $w$.

This keeps optimization simple.

---

# Polynomial Basis Functions

A common choice:

$$\Large
\phi_j(x)=x^j
$$

giving:

$$\Large
f(x)=w_0+w_1x+w_2x^2+\dots+w_Mx^M
$$

---

# Other Basis Functions

## Gaussian Basis

$$\Large
\phi_j(x)
=
e^{-\frac{(x-\mu_j)^2}{2s^2}}
$$

---

## Logistic Sigmoid

$$\Large
\phi_j(x)
=
\sigma\left(\frac{x-\mu_j}{s}\right)
$$

where:

$$\Large
\sigma(a)=\frac1{1+e^{-a}}
$$

---

# Main Idea

Basis functions map simple inputs into richer feature spaces.