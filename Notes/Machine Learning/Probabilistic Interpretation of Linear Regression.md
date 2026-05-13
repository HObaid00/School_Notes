# Probabilistic Interpretation of Linear Regression

Linear regression can also be viewed probabilistically.

---

# Generative Assumption

Assume:

$$\Large
y_i
=
f_w(x_i)+\epsilon_i
$$

where noise satisfies:

$$\Large
\epsilon_i\sim\mathcal{N}(0,\beta^{-1})
$$

This means targets are Gaussian-distributed:

$$\Large
y_i\sim\mathcal{N}(f_w(x_i),\beta^{-1})
$$

---

# Likelihood

The likelihood of the dataset is:

$$\Large
p(y|X,w,\beta)
=
\prod_{i=1}^{N}
p(y_i|x_i,w,\beta)
$$

![[Pasted image 20260506194359.png]]

---

# Maximum Likelihood Estimation

MLE chooses parameters maximizing likelihood:

$$\Large
w_{ML}
=
\arg\max_w p(y|X,w,\beta)
$$

---

# Important Result

Maximizing likelihood is mathematically equivalent to minimizing least squares loss.

Thus:

$$\Large
w_{ML}
=
(\Phi^T\Phi)^{-1}\Phi^Ty = \Phi^\dagger y
$$

---

# Big Insight

Least squares regression is not just an optimization trick.

It corresponds to a statistical noise model.

---
# Links
[[Machine Learning]]
[[Maximum likelihood Estimation (MLE)]]
[[Linear Regression]]
[[Moore-Penrose Pseudo Inverse]]
