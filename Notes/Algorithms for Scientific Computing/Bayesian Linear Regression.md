# Bayesian Linear Regression

Instead of estimating a single weight vector, Bayesian regression models uncertainty over weights.

---

# Prior Distribution

Assume weights follow a Gaussian prior:

$$\Large
p(w|\alpha)
=
\mathcal{N}(w|0,\alpha^{-1}I)
$$

This prior prefers small weights.

---

# Posterior Distribution

Using Bayes' theorem:

$$\Large
p(w|X,y)
\propto
p(y|X,w)p(w)
$$

---

# MAP Estimation

The maximum a posteriori estimate is:

$$\Large
w_{MAP}
=
\arg\max_w p(w|X,y)
$$

---

# Key Result

MAP estimation with Gaussian prior becomes ridge regression.

Specifically:

$$\Large
E_{MAP}(w)
\propto
E_{ridge}(w)
$$

with:

$$\Large
\lambda=\frac{\alpha}{\beta}
$$

---

# Full Bayesian Prediction

Instead of using a single estimate, Bayesian regression integrates over all possible weights.

This produces:

- uncertainty estimates
- more robust predictions
- confidence intervals

---

# Main Idea

Bayesian regression models uncertainty explicitly rather than pretending parameters are known exactly.

---
# Links
[[Bayesian Inference]]
[[Linear Regression]]
[[Maximum a Posteri Estimation (MAP)]]
[[Machine Learning]]