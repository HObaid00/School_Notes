# Generative Models and Linear Discriminant Analysis (LDA)

LDA is a probabilistic generative classifier.

---

# Assumptions

For each class:

$$\Large
p(x|y=c)
=
\mathcal{N}(x|\mu_c,\Sigma)
$$

where:

- $\mu_c$ = class mean
- $\Sigma$ = shared covariance matrix

---

# Shared Covariance

All classes share the same covariance matrix:

$$\Large
\Sigma
$$

This simplifies estimation and produces linear boundaries.

---

# Posterior Probability

For two classes:

$$\Large
p(y=1|x)
=
\sigma(w^Tx+w_0)
$$

where:

$$\Large
\sigma(a)=\frac1{1+e^{-a}}
$$

---

# Important Result

Gaussian class-conditionals with shared covariance lead to linear decision boundaries.

---

# LDA Parameters

The weights become:

$$\Large
w=\Sigma^{-1}(\mu_1-\mu_0)
$$

---

# Multiclass LDA 

$$\Large
p(y=c|x)
=
\frac{\exp(w_c^T x + w_{c0})}
{\sum_{c'} \exp(w_{c'}^T x + w_{c'0})}
$$

Softmax function:

$$\Large
\sigma(x)_i
=
\frac{\exp(x_i)}
{\sum_{k=1}^K \exp(x_k)}
$$

![[Pasted image 20260227224452.png]]

* Left:
	* $p(x\ | \ y = 1)$ - red
	* $p(x \ | \ y = 0)$ - blue
*  Right:
	* $p(y=1 \ | \ x)$ 

---

# Interpretation

The classifier compares distances to class distributions.

---
# Links
[[Machine Learning]]