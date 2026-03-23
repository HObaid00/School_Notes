**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
Winter Term 2025/2026  

---

# Motivation

Many machine learning tasks are optimization problems.

Examples:

- Linear Regression  
  $$\Large
  w^* = \arg\min_w \frac{1}{2}(Xw - y)^T (Xw - y)
  $$

- Logistic Regression  
  $$\Large
  w^* = \arg\min_w -\ln p(y \mid w, X)
  $$

Other examples:

- Support Vector Machines (maximum margin)
- k-means (minimize squared distances)
- Matrix Factorization (minimize reconstruction error)
- Neural Networks (minimize loss)
- And many more

---

# General Optimization Problem

Let:

- $\theta$ = parameters to optimize  
- $\mathcal{X}$ = domain (constraints on $\theta$)  
- $f(\theta)$ = objective function  

Goal:

$$\Large
\theta^* = \arg\min_{\theta \in \mathcal{X}} f(\theta)
$$

We seek a **global minimum**.

---

# Introductory Example

Unconstrained differentiable function:

$$\Large
f(\theta)
=
0.6 \theta^4
- 5 \theta^3
+ 13 \theta^2
- 12 \theta
+ 5
$$

Necessary condition for minima:

$$\Large
\nabla f(\theta) = 0
$$

Challenge: multiple local minima may exist.
![[Pasted image 20260228143217.png|697]]

---

# Convexity: Sets

A set $\mathcal{X}$ is convex iff:

$$\Large
\forall x,y \in \mathcal{X},\;
\lambda x + (1-\lambda)y \in \mathcal{X}
\quad \text{for } \lambda \in [0,1]
$$

![[Pasted image 20260228143236.png|697]]

---

# Convexity: Functions

A function $f$ is convex on convex set $\mathcal{X}$ iff:

$$\Large
f(\lambda x + (1-\lambda)y)
\le
\lambda f(x) + (1-\lambda)f(y)
$$

for all $x,y \in \mathcal{X}$ and $\lambda \in [0,1]$.

![[Pasted image 20260228143300.png|697]]

---

# Convexity and Minimization

Properties:

- Region above convex function is convex
- Convex functions have no local minima that are not global
- If $f$ convex and:
  $$\Large
  \nabla f(\theta^*) = 0
  $$
  then $\theta^*$ is a global minimum

Convex optimization is therefore “relatively easy”.
Convex:
![[Pasted image 20260228143710.png|697]]

Concave:
![[Pasted image 20260228143738.png|697]]

---

# First-Order Convexity Condition

Theorem:

$f$ differentiable and $\mathcal{X}$ convex.

Then $f$ is convex iff:

$$\Large
f(y)
\ge
f(x) + (y-x)^T \nabla f(x)
$$

for all $x,y \in \mathcal{X}$.

---

# Verifying Convexity

Ways to verify:

1. Use definition directly  
2. Use special results:
   - $f''(x) \ge 0$ (1D case)
   - Hessian positive semidefinite:
     $$\Large
     \nabla^2 f(x) \succeq 0
     $$
3. Use convexity-preserving operations

---

# Convexity-Preserving Operations

If $f_1, f_2$ convex:

- $f_1 + f_2$ is convex  
- $\max\{f_1, f_2\}$ is convex  
- $c f_1$ convex for $c \ge 0$  
- $f_1(Ax+b)$ convex  
- Composition with non-decreasing convex function  

---

# Convex Sets

- Intersection of convex sets is convex:

$$\Large
A, B \text{ convex}
\Rightarrow
A \cap B \text{ convex}
$$

![[Pasted image 20260228145519.png|697]]

---

# Easy Case

If:

- $f$ convex
- $f$ differentiable everywhere
- Analytical solution for $\nabla f(\theta)=0$ exists
- No constraints

Then we are done.

Example: Ordinary Least Squares.

---

# Harder Cases

Problems may involve:

- No closed-form solution (e.g. Logistic Regression)
- Constraints
- Non-differentiability
- Non-convexity

→ Need numerical methods.

---

# One-Dimensional Optimization

Idea:

- Solve $\Large \nabla f(\theta)=0$
- Use interval bisection if derivative monotonic

Algorithm:

Initialize $\Large A=a$, $\Large B=b$

Repeat:

- If $\Large f'(\frac{A+B}{2}) > 0$: set $B = \frac{A+B}{2}$
- Else: set $\Large A = \frac{A+B}{2}$

Stop when precision criterion satisfied.

Output:

$$\Large
x = \frac{A+B}{2}
$$

*(Copy algorithm diagram on slides 20–22.)*

---

# Gradient Descent (GD)

Idea:

- Gradient = steepest ascent
- Move in negative gradient direction

Algorithm:

Given $\theta^{(0)}$

Repeat:

1. $\Large \Delta \theta := -\nabla f(\theta)$
2. Line search:
   $$\Large
   t^* = \arg\min_{t>0} f(\theta + t\Delta\theta)
   $$
3. Update:
   $$\Large
   \theta \leftarrow \theta + t^*\Delta\theta
   $$

Until convergence.

---

# Convergence (Strongly Convex Case)

Residual error:

$$\Large
\rho =
f(\theta^{(k)}) - p^*
\le
c^k (f(\theta^{(0)}) - p^*)
$$

with $c < 1$.

Linear convergence:

$$\Large
k \sim \log(\rho^{-1})
$$

---

# Fixed Learning Rate

Avoid line search:

$$\Large
\theta_{t+1}
=
\theta_t - \tau \nabla f(\theta_t)
$$

$$\Large \tau = learning \space rate.$$

Problems:

- Too small → slow
- Too large → oscillations

![[Pasted image 20260228145552.png|697]]

---

# Learning Rate Schedule

Decrease learning rate:

$$\Large
\tau_{t+1} = \alpha \tau_t
\quad (0 < \alpha < 1)
$$

Require:

$$\Large
\lim_{t\to\infty} \tau_t = 0
$$

---

# Momentum

$$\Large
m_t
=
\tau \nabla f(\theta_t)
+
\gamma m_{t-1}
$$

$$\Large
\theta_{t+1}
=
\theta_t - m_t
$$

Accelerates in consistent directions.

---

# AdaGrad

- Parameter-specific learning rates
- Learning rate decreases with accumulated squared gradients

---

# Adam

First moment:

$$\Large
m_t = \beta_1 m_{t-1} + (1-\beta_1)\nabla f(\theta_t)
$$

Second moment:

$$\Large
v_t = \beta_2 v_{t-1} + (1-\beta_2)(\nabla f(\theta_t))^2
$$

Bias correction:

$$\Large
\hat m_t = \frac{m_t}{1-\beta_1^t}
$$

$$\Large
\hat v_t = \frac{v_t}{1-\beta_2^t}
$$

Update:

$$\Large
\theta_{t+1}
=
\theta_t
-
\frac{\tau}{\sqrt{\hat v_t}+\epsilon}
\hat m_t
$$

Defaults:

- $\Large\beta_1 = 0.9$
- $\Large\beta_2 = 0.999$
- $\Large\epsilon = 10^{-8}$

![[Pasted image 20260228145637.png|697]]
*https://ruder.io/optimizing-gradient-descent/*

---

# Newton Method

Second-order method.

Taylor expansion:

$$\Large
f(\theta_t + \delta)
=
f(\theta_t)
+
\delta^T \nabla f(\theta_t)
+
\frac{1}{2}
\delta^T \nabla^2 f(\theta_t)\delta
$$

Update:

$$\Large
\theta_{t+1}
=
\theta_t
-
[\nabla^2 f(\theta_t)]^{-1}
\nabla f(\theta_t)
$$

Pros:

- Fast convergence

Cons:

- Hessian $\Large O(d^2)$
- Inversion $\Large O(d^3)$

Use for low dimensions.

---

# Large-Scale Optimization

Higher-order methods too expensive.

Use first-order methods.

Still costly → Stochastic Optimization.

---

# Stochastic Gradient Descent (SGD)

Objective:

$$\Large
f(\theta)
=
\sum_{i=1}^n L_i(\theta)
$$

Approximate gradient using mini-batch $S$:

$$\Large
\theta_{t+1}
=
\theta_t
-
\tau
\frac{n}{|S|}
\sum_{j\in S}
\nabla L_j(\theta_t)
$$

Original SGD: $\Large |S|=1$

Full pass over dataset = epoch.

Convergence (convex case):

$$\Large
\mathbb{E}[\rho] \sim t^{-1}
$$

---

# Example: Perceptron via SGD

Classifier:

$$\Large
\delta(x)
=
\begin{cases}
1 & w^T x + b > 0 \\
-1 & \text{else}
\end{cases}
$$

Loss:

$$\Large
L(u,v)
=
\max(0, \epsilon - uv)
$$

SGD update:

If:

$$\Large
y_i(w^T x_i + b) < \epsilon
$$

then:

$$\Large
w \leftarrow w + \tau n y_i x_i
$$

$$\Large
b \leftarrow b + \tau n y_i
$$

---

# Optimizing Logistic Regression

Objective:

$$\Large
E(w)
=
-
\sum_{i=1}^N
\left[
y_i \ln \sigma(w^T x_i)
+
(1-y_i)\ln(1-\sigma(w^T x_i))
\right]
$$

No closed form solution.

Use:

- Gradient descent
- SGD
- Add regularization:
  $$\Large
  E_{reg}(w) = E(w) + \lambda \|w\|_2^2
  $$

---

# Distributed Learning

Large-scale problems → multiple machines.

Two paradigms:

## Data Parallelism

- Multiple model replicas
- Process different data subsets
- Synchronize via parameter server

## Model Parallelism

- Split model across machines
- Exploit structure (e.g. CNNs, matrix factorization)

*(Copy data vs model parallelism diagram on slide 49.)*
![[Pasted image 20260228145754.png|325]]
![[Pasted image 20260228145810.png|326]]

---

# Parameter Server

Goal:

- Communication time << computation time

Workers:

- Compute gradients
- Send updates
- Receive updated parameters

![[Pasted image 20260228145859.png]]

---

# Summary

- Optimization: find $\theta^*$ minimizing $f$
- Convexity → global optimality
- Gradient Descent:
  $$\Large
  \theta \leftarrow \theta - t\nabla f(\theta)
  $$
- Learning rate selection critical
- SGD: mini-batch updates
- Distributed learning: data & model parallelism

---

# Reading

Boyd — *Convex Optimization*  
Ch. 2.1–2.3, 3.1, 3.2, 4.1, 4.2, 9

Sebastian Ruder —  
“An overview of gradient descent optimization algorithms”  
https://arxiv.org/abs/1609.04747