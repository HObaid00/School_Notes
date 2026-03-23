**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
Winter Term 2025/2026  

---

# Notation

| Symbol | Meaning |
|--------|---------|
| $x$ | scalar (lowercase, not bold) |
| $\mathbf{x}$ | vector (lowercase, bold) |
| $\mathbf{\Sigma}$ | matrix (uppercase, bold) |
| $f(x)$ | predicted value for input $x$ |
| $\mathbf{y}$ | vector of targets |
| $y_i$ | target of the $i$-th example |
| $w_0$ | bias term |
| $\phi(\cdot)$ | basis function |
| $E(\cdot)$ | error function |
| $\mathcal{D}$ | training data |
| $X^\dagger$ | Moore–Penrose pseudoinverse |

Bias term is assumed to be absorbed unless stated otherwise.

---

# 1. Basic Linear Regression

## Regression Problem

Given:

- Observations  
  $$\Large
  X = \{x_1, \dots, x_N\}, \quad x_i \in \mathbb{R}^D
  $$

- Targets  
  $$\Large
  y = \{y_1, \dots, y_N\}, \quad y_i \in \mathbb{R}
  $$

Find mapping:

$$\Large
y_i \approx f(x_i)
$$

---

## Linear Model

Assume:

$$\Large
y_i = f(x_i) + \varepsilon_i,
\quad \varepsilon_i \sim \mathcal{N}(0, \beta^{-1})
$$

Choose linear function:

$$\Large
f_w(x_i) = w_0 + w_1 x_{i1} + \dots + w_D x_{iD}
$$

Compact form:

$$\Large
f_w(x_i) = w_0 + w^T x_i
$$

---

## Absorbing the Bias

Define:

$$\Large
\tilde{x} = (1, x_1, \dots, x_D)^T
$$

$$\Large
\tilde{w} = (w_0, w_1, \dots, w_D)^T
$$

Then:

$$\Large
f_w(x) = \tilde{w}^T \tilde{x}
$$

From now on, assume bias is absorbed.

---

# Least Squares Loss

$$\Large
E_{LS}(w) =
\frac{1}{2}
\sum_{i=1}^N
(w^T x_i - y_i)^2
$$

Matrix form:

$$\Large
E_{LS}(w) =
\frac{1}{2}
(Xw - y)^T (Xw - y)
$$

---

# Optimal Solution

Gradient:

$$\Large
\nabla_w E_{LS}(w)
=
X^T X w - X^T y
$$

Set to zero:

$$\Large
X^T X w - X^T y = 0
$$

Normal equation:

$$\Large
w^* =
(X^T X)^{-1} X^T y
=
X^\dagger y
$$

---

# Nonlinear Dependencies

Example data:

$$\Large
y_i = \sin(2\pi x_i) + \varepsilon_i
$$

Use polynomial basis:

$$\Large
f_w(x) =
w_0 + \sum_{j=1}^M w_j x^j
$$

General basis representation:

$$\Large
f_w(x) =
w^T \phi(x)
$$

Model is linear in $w$, nonlinear in $x$.

---

# Typical Basis Functions

- Polynomial:
  $$\Large
  \phi_j(x) = x^j
  $$

- Gaussian:
  $$\Large
  \phi_j(x) =
  \exp\left(
  -\frac{(x-\mu_j)^2}{2s^2}
  \right)
  $$

- Logistic sigmoid:
  $$\Large
  \phi_j(x) =
  \sigma\left(
  \frac{x-\mu_j}{s}
  \right),
  \quad
  \sigma(a) = \frac{1}{1+e^{-a}}
  $$

---

# Design Matrix

Define:

$$\Large
\Phi \in \mathbb{R}^{N \times (M+1)}
$$

Loss:

$$\Large
E_{LS}(w) =
\frac{1}{2}
(\Phi w - y)^T (\Phi w - y)
$$

Solution:

$$\Large
w^* =
(\Phi^T \Phi)^{-1} \Phi^T y
=
\Phi^\dagger y
$$

---

# Choosing Polynomial Degree $M$

Use train-validation split.

*(Copy polynomial degree comparison plots on slides 17–22.)*

Observation:

- Small $M$ → underfitting  
- Large $M$ → overfitting  

---

# Regularization (Ridge Regression)

Add L2 penalty:

$$\Large
E_{\text{ridge}}(w)
=
\frac{1}{2}
\sum_{i=1}^N
(w^T \phi(x_i) - y_i)^2
+
\frac{\lambda}{2}
\|w\|_2^2
$$

where:

$$\Large
\|w\|_2^2 = w^T w
$$

Large $\lambda$ → smaller weights → less variance.

---

# Bias-Variance Tradeoff

Error decomposes into:

- **Bias**: model mismatch  
- **Variance**: sensitivity to training data  

High bias:

- Model too rigid  
- $\lambda$ too large  

High variance:

- Model too flexible  
- $\lambda$ too small  

*(Copy bias-variance target plots on slides 26–28.)*

---

# Correlation

Linear fit example:

$$\Large
f(x) = 0.018x + 13.43
$$

Weights reflect strength of linear relationship.

Normalize data to handle scale differences.

---

# Correlation vs. Causation

Correlation does not imply causation.

Beware of confounding variables.

---

# 2. Probabilistic Linear Regression

Assume:

$$\Large
y_i \sim
\mathcal{N}(f_w(x_i), \beta^{-1})
$$

Likelihood:

$$\Large
p(y | X, w, \beta)
=
\prod_{i=1}^N
\mathcal{N}(y_i | w^T \phi(x_i), \beta^{-1})
$$

---

# Maximum Likelihood

Maximize:

$$\Large
\ln p(y | X, w, \beta)
$$

Equivalent to minimizing:

$$\Large
E_{LS}(w)
$$

Thus:

$$\Large
w_{ML}
=
(\Phi^T \Phi)^{-1} \Phi^T y
$$

Estimate precision:

$$\Large
\frac{1}{\beta_{ML}}
=
\frac{1}{N}
\sum_{i=1}^N
(w_{ML}^T \phi(x_i) - y_i)^2
$$

---

# Bayesian Linear Regression

Posterior:

$$\Large
p(w | X, y, \beta)
\propto
p(y | X, w, \beta)
p(w)
$$

Choose Gaussian prior:

$$\Large
p(w | \alpha)
=
\mathcal{N}(w | 0, \alpha^{-1} I)
$$

---

# MAP Estimation

Minimize:

$$\Large
E_{MAP}(w)
=
\frac{\beta}{2}
\sum_{i=1}^N
(w^T \phi(x_i) - y_i)^2
+
\frac{\alpha}{2}
\|w\|_2^2
$$

Equivalent to ridge regression with:

$$\Large
\lambda = \frac{\alpha}{\beta}
$$

---

# Full Bayesian Posterior

Posterior:

$$\Large
p(w | D)
=
\mathcal{N}(w | \mu, \Sigma)
$$

where:

$$\Large
\Sigma^{-1}
=
\alpha I + \beta \Phi^T \Phi
$$

$$\Large
\mu
=
\beta \Sigma \Phi^T y
$$

Observations:

- $w_{MAP} = \mu$
- $\alpha \to 0$ → ML solution
- $N=0$ → posterior equals prior

---

# Prediction

MLE:

$$\Large
p(\hat{y}_{new} | x_{new})
=
\mathcal{N}
(w_{ML}^T \phi(x_{new}), \beta^{-1})
$$

MAP:

$$\Large
p(\hat{y}_{new} | x_{new})
=
\mathcal{N}
(w_{MAP}^T \phi(x_{new}), \beta^{-1})
$$

---

# Posterior Predictive Distribution

$$\Large
p(\hat{y}_{new} | x_{new}, D)
=
\mathcal{N}
\left(
\mu^T \phi(x_{new}),
\beta^{-1}
+
\phi(x_{new})^T
\Sigma
\phi(x_{new})
\right)
$$

Variance now depends on $x_{new}$.

![[Pasted image 20260227102219.png]]

---

# Summary

- Least squares ⇔ Maximum likelihood  
- Ridge regression ⇔ MAP  
- Linear in weights, nonlinear in input possible  
- Regularization controls overfitting  
- Full Bayesian gives uncertainty estimates  

---

# Reading

**Main:**

- Bishop — *Pattern Recognition and Machine Learning*  
  (Ch. 1.1, 3.1–3.3, 3.6)

**Extra:**

- Murphy — *Machine Learning: A Probabilistic Perspective*  
  (Ch. 7.2–7.3, 7.5–7.6)