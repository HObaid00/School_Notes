**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning Group  
Technical University of Munich  
Winter Term 2025/2026  

---

# Section 1: Introduction

## Logistic Regression Revisited

Logistic regression models:

$$\Large
y \mid x \sim \text{Bernoulli}(\sigma(w^T x))
$$

where:

$$\Large
w^T x = w_0 + \sum_{j=1}^{D} w_j x_j
$$

$$\Large
\sigma(a) = \frac{1}{1 + e^{-a}}
$$

Graphical interpretation:

- Nodes = scalar inputs (including bias $x_0 = 1$)
- Weighted sum:
  $$\Large
  a = \sum_{j=0}^{D} w_j x_j
  $$
- Activation:
  $$\Large
  p(y=1 \mid x) = \sigma(a)
  $$

---

## XOR Dataset

XOR is **not linearly separable**.

→ Logistic regression fails because it learns a linear decision boundary.

*(Copy XOR illustration on slide 4.)*

---

# Handling Non-Linearity with Basis Functions

Model:

$$\Large
f(x,w)
=
\sigma\left(
w_0 + \sum_{j=1}^{M-1} w_j \phi_j(x)
\right)
=
\sigma(w^T \phi(x))
$$

- $\phi(x)$ = nonlinear basis functions
- Still linear in $w$
- $\phi$ maps data into space where it becomes linearly separable

---

## Example: Custom Basis for XOR

Define transformation:

$$\Large
\phi(x)
=
\left(
\sigma(5 + x_1 + x_2),
\sigma(5 - x_1 - x_2)
\right)
$$

Overall model:

$$\Large
f(x,w) = \sigma(w^T \phi(x))
$$

Train via binary cross-entropy:

$$\Large
w^*
=
\arg\min_w
\sum_{n=1}^{N}
-
\left[
y_n \log f(x_n,w)
+
(1-y_n)\log(1-f(x_n,w))
\right]
$$
![[Pasted image 20260228150017.png|697]]
Here we defined a **custom basis function** $\Large \phi : \mathbb{R}^3 \rightarrow \mathbb{R}^2$

---

# Learning Basis Functions Automatically

Instead of hand-designing $\phi$, learn it jointly with $w$.

Example: Feed-Forward Neural Network (1 hidden layer):

$$\Large
f(x,W)
=
\sigma_1
\left(
W_1
\sigma_0
(W_0 x)
\right)
$$

Train all weights:

$$\Large
W^*
=
\arg\min_W
\sum_{n=1}^{N}
-
\left[
y_n \log f(x_n,W)
+
(1-y_n)\log(1-f(x_n,W))
\right]
$$

---

# Deep Neural Networks (MLP)

By stacking layers:

$$\Large
f(x,W,b)
=
\sigma_2(
W_2 \sigma_1(
W_1 \sigma_0(W_0 x + b_0)
+ b_1)
+ b_2)
$$

- $\Large W = \{W_0, W_1, W_2\}$
- $\Large b = \{b_0, b_1, b_2\}$

This is a **Multi-Layer Perceptron (MLP)**.
![[Pasted image 20260228151700.png|697]]

---

# Activation Functions

Common activation functions (element-wise):

- Sigmoid:
  $$\Large
  \sigma(x) = \frac{1}{1+e^{-x}}
  $$

- tanh:
  $$\Large
  \tanh(x)
  $$

- ReLU:
  $$\Large
  \max(0,x)
  $$

- Leaky ReLU:
  $$\Large
  \max(0.1x,x)
  $$

- ELU
- Swish:
  $$\Large
  x \cdot \sigma(x)
  $$

Softmax is applied over vectors (not element-wise).

![[Pasted image 20260228151726.png]]

---

# Why Nonlinear Activations?

If all layers are linear:

$$\Large
f(x) = W_L W_{L-1} \dots W_0 x
= W' x
$$

Equivalent to single linear transformation.

With nonlinear activations:

$$\Large
f(x) \neq W' x
$$

→ Enables learning complex functions.

---

# Universal Approximation Theorem

An MLP with:

- One hidden layer
- Sufficient hidden units
- Suitable activation (e.g. sigmoid)

can approximate any continuous function on compact domains.

Good news: expressive power.  
Bad news: training is hard.

---

# Why Multiple Hidden Layers?

Although 1 hidden layer suffices theoretically:

- Some functions require exponentially many neurons with shallow networks.
- Deep networks can represent them more compactly.
- Learn hierarchical representations.
![[Pasted image 20260228151816.png|401]]


---

# Section 2: Beyond Binary Classification

## Choosing Output Activation and Loss

| Task | Distribution | Final Activation | Loss |
|------|--------------|------------------|------|
| Binary | Bernoulli | Sigmoid | Binary cross entropy |
| Multi-class | Categorical | Softmax | Cross entropy |
| Regression | Gaussian | Identity | Squared error |

---

## Binary Classification

Activation:

$$\Large
f(x,W) = \sigma(a)
$$

Loss:

$$
E(W)
=
-
\sum_{n=1}^{N}
\left[
y_n \log f(x_n,W)
+
(1-y_n)\log(1-f(x_n,W))
\right]
$$

---

## Multi-Class Classification

Softmax:

$$\Large
f_k(x,W)
=
\frac{e^{a_k}}{\sum_{j=1}^K e^{a_j}}
$$

Loss:

$$\Large
E(W)
=
-
\sum_{n=1}^{N}
\sum_{k=1}^{K}
y_{nk} \log f_k(x_n,W)
$$

---

## Regression

Output:

$$\Large
f(x,W) = a
$$

Loss:

$$\Large
E(W)
=
\sum_{n=1}^{N}
(y_n - f(x_n,W))^2
+ \text{const.}
$$

---

# Unsupervised Deep Learning

Examples:

- Autoencoders
- Variational Autoencoders
- GANs
- Representation learning (embeddings)

---

# Choosing the Loss

Examples:

- Cross entropy
- MSE
- MAE
- Huber
- LogCosh
- Wasserstein distance
- KL-divergence

---

# Section 3: Parameter Learning

## Optimization

Loss:

$$\Large
E(W)
$$

Usually **non-convex**.

Gradient descent:

$$\Large
W \leftarrow W - \tau \nabla_W E(W)
$$

Local minima acceptable if generalization good.

---

# Computing the Gradient

Options:

1. Manual differentiation
2. Numerical differentiation
   $$\Large
   \frac{\partial E}{\partial w}
   \approx
   \frac{E(w+\epsilon)-E(w)}{\epsilon}
   $$
   → $O(|W|^2)$
3. Symbolic differentiation
4. Automatic differentiation (Backpropagation)
   → $O(|W|)$

---

# Backpropagation (Toy Example)

$$\Large
f(x) = \frac{2}{\sin(\exp(-x))}
$$

Chain rule:

$$\Large
\frac{\partial f}{\partial x}
=
\frac{\partial d}{\partial c}
\frac{\partial c}{\partial b}
\frac{\partial b}{\partial a}
\frac{\partial a}{\partial x}
$$

Forward pass: compute and cache intermediate values.  
Backward pass: multiply local derivatives.

![[Pasted image 20260228151857.png|697]]

---

# Multiple Paths

If multiple paths from $x$ to $c$:

$$\Large
\frac{\partial c}{\partial x}
=
\sum_i
\frac{\partial c}{\partial a_i}
\frac{\partial a_i}{\partial x}
$$

Multivariate chain rule.

---

# Jacobian and Gradient

For:

$$\Large
f : \mathbb{R}^n \to \mathbb{R}^m
$$

Jacobian:

$$\Large
\frac{\partial a}{\partial x}
\in \mathbb{R}^{m \times n}
$$

Gradient:

$$\Large
\nabla_a c
=
\left(
\frac{\partial c}{\partial a}
\right)^T
$$

Matrix chain rule:

$$\Large
\nabla_x c
=
\left(
\frac{\partial a}{\partial x}
\right)^T
\nabla_a c
$$

---

# Backprop in Neural Networks

Example network:

$$\Large
a = Wx + b
$$

$$\Large
h = \sigma(a)
$$

$$\Large
\hat{y} = Vh + c
$$

$$\Large
E = (\hat{y} - y)^2
$$

We compute:

$$\Large
\frac{\partial E}{\partial W}
=
\frac{\partial E}{\partial \hat{y}}
\frac{\partial \hat{y}}{\partial h}
\frac{\partial h}{\partial a}
\frac{\partial a}{\partial W}
$$

---

# Affine Layer Gradients

For:

$$\Large
a = Wx + b
$$

Forward:

$$\Large
a = Wx + b
$$

Backward:

$$\Large
\frac{\partial E}{\partial W}
=
\left(
\frac{\partial E}{\partial a}
\right)^T x^T
$$

$$\Large
\frac{\partial E}{\partial x}
=
W^T
\frac{\partial E}{\partial a}
$$

$$\Large
\frac{\partial E}{\partial b}
=
\frac{\partial E}{\partial a}
$$

Vectorized implementation is efficient.

---

# Backpropagation Summary

- Represent computation as graph
- Forward pass: compute outputs
- Backward pass: accumulate gradients
- Avoid explicit Jacobian construction
- Each neuron visited twice

---

# Reading

Goodfellow et al., *Deep Learning* — Chapter 6

Acknowledgements:

- Patrick van der Smagt
- Peter Bloem (mlvu.github.io)