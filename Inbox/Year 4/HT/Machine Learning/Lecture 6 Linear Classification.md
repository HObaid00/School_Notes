**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
Winter Term 2025/2026  

---

# Notation

| Symbol                 | Meaning                                    |
| ---------------------- | ------------------------------------------ |
| $\Large s$             | scalar (lowercase, not bold)               |
| $\Large \mathbf{s}$    | vector (lowercase, bold)                   |
| $\Large \mathbf{S}$    | matrix (uppercase, bold)                   |
| $\Large \hat{y}$       | predicted class label                      |
| $\Large y$             | actual class label                         |
| $\Large \mathbb{I}(a)$ | Indicator function (1 if $a$ true, else 0) |

Bias term $w_0$ is assumed absorbed unless stated otherwise.

---

# 1. Introduction to Linear Classification

## Classification vs Regression

**Regression**

- $y \in \mathbb{R}$ (continuous)
- Example: house price prediction

**Classification**

- $y \in \{1, \dots, C\}$
- Example: cat vs dog classification

---

## Classification Problem

Given:

$$\Large
X = \{x_1, \dots, x_N\}, \quad x_i \in \mathbb{R}^D
$$

Classes:

$$\Large
\mathcal{C} = \{1, \dots, C\}
$$

Labels:

$$\Large
y = \{y_1, \dots, y_N\}, \quad y_i \in \mathcal{C}
$$

Find:

$$\Large
f : \mathbb{R}^D \to \mathcal{C}
$$

such that:

$$\Large
y_i = f(x_i)
$$
![[Pasted image 20260227105035.png]]

---

## Zero-One Loss

$$\Large
\ell_{01}(y, \hat{y})
=
\sum_{i=1}^N
\mathbb{I}(\hat{y}_i \ne y_i)
$$

Counts misclassified samples.

---

# Hyperplane as Decision Boundary

For binary classification $C = \{0,1\}$:

Define hyperplane:

$$\Large
w^T x + w_0 = 0
$$

Classification rule:

$$\Large
w^T x + w_0
\begin{cases}
= 0 & \text{on plane} \\
> 0 & \text{normal side} \\
< 0 & \text{other side}
\end{cases}
$$

Signed distance:

$$\Large
r = \frac{y(x)}{\|w\|}
$$

Dataset $\Large D = \{(\mathbf{x_i}, y_i)\}$ is **linearly separable** if such a hyperplane exists. for which all $\mathbf{x_i}$ with $y_i = 0$ are on one and all $\mathbf{x_i}$ with $y_i = 1$ on the other side   

![[Pasted image 20260227105524.png]]

---

# Perceptron

Decision rule:

$$\Large
\hat{y} = f(w^T x + w_0)
$$

Step function:

$$\Large
f(t) =
\begin{cases}
1 & t > 0 \\
0 & \text{otherwise}
\end{cases}
$$



---

## Perceptron Learning Rule

Initialize:

$$\Large
w, w_0 \leftarrow 0
$$

For each misclassified sample:

$$\Large
w \leftarrow
\begin{cases}
w + x_i & y_i = 1 \\
w - x_i & y_i = 0
\end{cases}
$$

$$\Large
w_0 \leftarrow
\begin{cases}
w_0 + 1 & y_i = 1 \\
w_0 - 1 & y_i = 0
\end{cases}
$$

Converges in finite steps if linearly separable.
![[Pasted image 20260227110151.png]]

---

# Multiclass Extensions

## One-vs-Rest

Train C classifiers:

$$
C_i \text{ vs not } C_i
$$

![[Pasted image 20260227105657.png]] 

---

## One-vs-One

Train classifier for each class pair.

Use majority vote.

![[Pasted image 20260227105719.png]]

---

## Multiclass Discriminant

Define:

$$\Large
f_c(x) = w_c^T x + w_{c0}
$$

Decision rule:

$$\Large
\hat{y} =
\arg\max_{c \in \mathcal{C}} f_c(x)
$$

Regions are convex.

![[Pasted image 20260227105746.png]]

---

# Nonlinear Decision Boundaries

Apply nonlinear feature map:

$$\Large
\phi : \mathbb{R}^D \to \mathbb{R}^M
$$

Example:

$$\Large
\phi(x) = (\theta, r) = (\text{angle}(x), \|x\|_2)
$$

Transforms data to linearly separable space.

![[Pasted image 20260227224307.png]]

---

# Limitations of Hard Decisions

- No uncertainty estimate  
- Poor handling of noise  
- Difficult optimization  
- Poor generalization  

![[Pasted image 20260227105923.png]]

---

# 2. Probabilistic Generative Models

Use Bayes rule:

$$\Large
p(y=c|x)
\propto
p(x|y=c) p(y=c)
$$

Components:

- Class prior $p(y=c)$  
- Class conditional $p(x|y=c)$  

---

## Learning Procedure

1. Choose parametric forms:
   - $p(x|y=c,\psi)$
   - $p(y=c|\theta)$
2. Estimate parameters via ML
3. Perform inference:

$$\Large
p(y=c|x)
\propto
p(x|y=c,\hat{\psi}) p(y=c|\hat{\theta})
$$

Also allows data generation.

---

## Class Prior

Categorical distribution:

$$\Large
y \sim \text{Categorical}(\theta)
$$

$$\Large
p(y=c) = \theta_c
$$

MLE:

$$\Large
\theta_c^{MLE}
=
\frac{1}{N}
\sum_{i=1}^N
\mathbb{I}(y_i = c)
$$

---

## Gaussian Class Conditionals

$$\Large
p(x|y=c)
=
\mathcal{N}(x|\mu_c,\Sigma)
$$

Shared covariance matrix $\Sigma$.

*(Copy Gaussian clusters illustration on slide 24.)*

---

# Posterior for C=2

$$\Large
p(y=1|x)
=
\frac{p(x|y=1)p(y=1)}
{p(x|y=1)p(y=1)+p(x|y=0)p(y=0)}
$$

Equivalent to:

$$\Large
p(y=1|x)
=
\frac{1}{1+\exp(-a)}
=
\sigma(a)
$$

where:

$$\Large
a
=
\log
\frac{p(x|y=1)p(y=1)}
{p(x|y=0)p(y=0)}
$$

---

# Linear Discriminant Analysis (LDA)

With shared covariance:

$$\Large
a = w^T x + w_0
$$

where:

$$\Large
w = \Sigma^{-1}(\mu_1 - \mu_0)
$$

$$\Large
w_0
=
-\frac{1}{2}
\mu_1^T \Sigma^{-1}\mu_1
+
\frac{1}{2}
\mu_0^T \Sigma^{-1}\mu_0
+
\log \frac{p(y=1)}{p(y=0)}
$$

Posterior:

$$\Large
p(y=1|x)
=
\sigma(w^T x + w_0)
$$
![[Pasted image 20260227224452.png]]

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

---

# Naive Bayes

Assume conditional independence:

$$\Large

p(x_1,\dots,x_d|y=c)
=
\prod_{i=1}^d
p(x_i|y=c)
$$

Gaussian case:

$$\Large
p(x|y=c)
=
\mathcal{N}(x|\mu_c,\Sigma_c)
$$

Different covariance per class.

Leads to **quadratic** boundary.

![[Pasted image 20260227224514.png]]

---

# 3. Probabilistic Discriminative Models

Instead of modeling $p(x|y)$, directly model:

$$\Large
p(y|x)
$$

---

# Logistic Regression

Model:

$$\Large
y|x
\sim
\text{Bernoulli}(\sigma(w^T x))
$$

Sigmoid:

$$\Large
\sigma(a)
=
\frac{1}{1+\exp(-a)}
$$

---

## Likelihood

$$\Large
p(y|w,X)
=
\prod_{i=1}^N
\sigma(w^T x_i)^{y_i}
(1-\sigma(w^T x_i))^{1-y_i}
$$

---

## Negative Log-Likelihood

$$\Large
E(w)
=
-
\sum_{i=1}^N
\Big[
y_i \log \sigma(w^T x_i)
+
(1-y_i)
\log (1-\sigma(w^T x_i))
\Big]
$$

Binary cross entropy loss.

No closed-form solution → numerical optimization.

---

## Regularized Logistic Regression

$$\Large
E(w)
=
-\log p(y|w,X)
+
\lambda \|w\|_q^q
$$

For $q=2$ → Gaussian prior → MAP estimate.

---

# Multiclass Logistic Regression

$$\Large
p(y=c|x)
=
\frac{\exp(w_c^T x)}
{\sum_{c'} \exp(w_{c'}^T x)}
$$

Loss:

$$\Large
E(w)
=
-
\sum_{i=1}^N
\sum_{c=1}^C
y_{ic}
\log p(y=c|x_i)
$$

Cross entropy with one-hot encoding:

$$\Large
y_{ic}
=
\begin{cases}
1 & \text{if sample } i \text{ in class } c \\
0 & \text{otherwise}
\end{cases}
$$

---

# Generative vs Discriminative

**Discriminative**

- Better pure classification performance

**Generative**

- Can generate data  
- Handle missing data  
- Semi-supervised learning  
- Outlier detection  

---

# Reading

Bishop — *Pattern Recognition and Machine Learning*  
Ch. 4.1–4.3