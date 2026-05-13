# Naive Bayes

Naive Bayes is a probabilistic generative classifier.

---

# Core Assumption

Features are conditionally independent given the class:

$$\Large
p(x_1,\dots,x_d|y=c)
=
\prod_{i=1}^{d}
p(x_i|y=c)
$$
In the case of continuous data where the likelihood is assumed to be a normal distribution, this corresponds to **diagonal** covariance matrices, i.e. **Gaussian Naive Bayes**

---

# Why "Naive"?

Because feature independence is often unrealistic.

Yet the method works surprisingly well in practice.

---

# Gaussian Naive Bayes

For continuous features:

$$\Large
p(x|y=c)
=
\mathcal{N}(x|\mu_c,\Sigma_c)
$$

with diagonal covariance matrices.

> Important: **Naive Bayes** uses a different covariance matrix $\Sigma_c$ for each class $c$!

---

# Difference from LDA

## LDA

 As mentioned in [[Generative Models and LDA]] LDA uses the same covariance matrix.

$$\Large
\Sigma
$$

---

## Naive Bayes

Uses class-specific covariance matrices:

$$\Large
\Sigma_c
$$

---

# Decision Boundary

Naive Bayes can produce quadratic boundaries.

![[Pasted image 20260227224514.png]]

LDA produces linear boundaries.

---

# Advantage

Naive Bayes easily handles mixed feature types:

- Gaussian
- categorical
- binary
- count data

---
# Links
[[Bayes sats]]
[[Bayesian Inference]]
[[Generative Models and LDA]]
[[Machine Learning]]

