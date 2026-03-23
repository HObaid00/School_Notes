**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning Group  
Technical University of Munich  
Winter Term 2025/2026  

---

# Roadmap

- Structured data  
- Training deep neural networks  
- Deep learning frameworks  
- Modern architectures & tricks  

---

# Section 1: Structured Data

## Different Layer Types

Beyond fully-connected layers, neural networks use specialized layers:

- Convolutional layers (images)
- Recurrent layers (sequences)
- Graph convolutional layers (graphs)
- Attention-based layers
- etc.

These layers introduce **inductive bias** by exploiting data structure.

---

# Neural Networks for Images

Example:

- Image: $\Large 100 \times 100$ pixels
- Single hidden layer with 1,000 units

Fully-connected approach:

- $\Large 100 \times 100 \times 1000 = 10^7$ parameters

Using convolution:

- $1,000$ filters of size $5 \times 5$
-  $1000 \cdot 25 = 25{,}000$ parameters

Key idea: exploit **local correlation** in images.

![[Pasted image 20260228151959.png|697]]

---

# CNN: Convolution

## Continuous Convolution

$$\Large
(x * k)(t)
=
\int_{-\infty}^{\infty}
x(\tau) k(t - \tau)\, d\tau
$$

Interpretation: weighted average of signal $x$ using kernel $k$.

---

## Discrete Convolution

$$\Large
(x * k)(t)
=
\sum_{\tau=-\infty}^{\infty}
x(\tau) k(t - \tau)
$$

---

## 2D Convolution (Images)

$$\Large
(x * k)(i,j)
=
\sum_l \sum_m
x(l,m) k(i-l, j-m)
$$

In practice, CNN libraries implement **cross-correlation**:

$$\Large
\hat{x}(i,j)
=
\sum_{l=1}^{L} \sum_{m=1}^{M}
x(i+l, j+m) k(l,m)
$$

With multiple channels:

Number of parameters:

$$\Large
L \times M \times C_{in} \times C_{out}
$$

Weights are shared across spatial positions.

![[Pasted image 20260228152037.png|697]]

---

# CNN: Padding

Boundary handling strategies:

- **VALID**:
  $$\Large
  D_{l+1} = (D_l - K) + 1
  $$

- **SAME**:
  $$\Large
  P = \lfloor K/2 \rfloor
  $$

- **FULL**:
  Add $K-1$ values per side

![[Pasted image 20260228152109.png]]
---

# CNN: Strides

Stride $S$ = step size of kernel.

Output size:

$$\Large
D_{l+1}
=
\left\lfloor
\frac{D_l + 2P - K}{S}
\right\rfloor + 1
$$

Strides $>1$ perform downsampling.
![[Pasted image 20260228181231.png|697]]

---

# CNN: Pooling

Computes summary statistics over local windows.

Examples:

- Max pooling
- Mean pooling
- $L_p$ pooling

Provides invariance to small shifts.
![[Pasted image 20260228181257.png|697]]

---

# CNN Architecture Example

Typical pipeline:

Conv → ReLU → Pool → Conv → Pool → Fully Connected → Output
![[Pasted image 20260228181322.png|697]]

---

# Architectures for Other Structured Data

- **RNNs**: sequential data (text, time series)
- **GNNs**: graph data (social networks, molecules)
- **Attention models / Transformers**: various data types
![[Pasted image 20260228181412.png]]

---

# Section 2: Training Deep Neural Networks

## Double Descent

Classical bias-variance tradeoff:

- More parameters → lower bias, higher variance
- Test error increases after certain complexity

Modern observation:

- Very large networks can achieve low training error
- Test error decreases again beyond interpolation threshold

This is called **double descent**.

![[Pasted image 20260228181453.png|697]]

---

# Weight Initialization

Training starts from initial weights.

Two key issues:

1. **Weight symmetry**
2. **Weight scale**

---

## Weight Symmetry

If two units have identical weights:

- They receive identical gradients
- Learn identical features

Solution:

- Initialize with small random values

---

## Weight Scale

Large fan-in or fan-out may cause:

- Saturation (sigmoid)
- Exploding gradients
- Vanishing gradients

---

# Xavier (Glorot) Initialization

Goal: preserve variance in forward and backward pass.

Set:

$$\Large
\text{Var}(W)
=
\frac{2}{\text{fan-in} + \text{fan-out}}
$$

Example distribution:

$$\Large
W
\sim
\text{Uniform}
\left(
-
\sqrt{\frac{6}{\text{fan-in}+\text{fan-out}}},
\sqrt{\frac{6}{\text{fan-in}+\text{fan-out}}}
\right)
$$

---

# Vanishing & Exploding Gradients

Repeated multiplication:

$$\Large
W^t = V (\text{diag}(D))^t V^{-1}
$$

If:

- $D_{ii} < 1$ → vanishing gradients
- $D_{ii} > 1$ → exploding gradients

Also caused by saturating activations.

Solutions:

- Better initialization
- Batch normalization
- Gradient clipping

---

# Regularization

Common techniques:

- L2 weight decay
- L1 regularization
- Early stopping
- Data augmentation
- Noise injection
- Parameter sharing
- Dropout

---

# Dropout

During training:

- Each hidden unit set to 0 with probability $p$ (e.g. 0.5)

Equivalent to sampling from $2^H$ architectures with shared weights.

![[Pasted image 20260228181529.png|697]]

---

# Hyperparameter Optimization

Tune:

- Number of layers
- Number of units
- Activation functions
- Optimizer
- Learning rate schedule
- Preprocessing

Methods:

- Random search
- Bayesian optimization

---

# Gradient-Based Hyperparameter Optimization

For continuous hyperparameters:

- Backpropagate through training procedure
- Update hyperparameters via gradient

Related concepts:

- Meta-learning
- Few-shot learning

Very expensive for large networks.

---

# Section 3: Deep Learning Frameworks

Popular libraries:

- PyTorch
- TensorFlow
- JAX
- MXNet

---

# Static vs Dynamic Computational Graphs

Frameworks build computational graphs.

## Static Graphs (Define-and-Run)

- Graph defined first
- Then executed
- Can be optimized (JIT)

## Dynamic Graphs (Define-by-Run)

- Graph created during execution
- More flexible (e.g., RNNs with variable length)

Modern frameworks mostly dynamic.

![[Pasted image 20260228181602.png]]

---

# Section 4: Modern Architectures & Tricks

## Batch Normalization

Normalize activations per mini-batch:

$$\Large
\hat{x}
=
\frac{x - \mathbb{E}_B[x]}
{\sqrt{\text{Var}_B[x] + \epsilon}}
$$

Add learnable parameters:

$$\Large
y = \gamma \hat{x} + \beta
$$

Benefits:

- Smoother loss landscape
- More stable gradients
- Faster convergence

---

## Other Normalization Methods

- Layer normalization
- Instance normalization
- Group normalization

---

# Skip Connections

## Highway Networks

$$\Large
y
=
f(x,W)T(x,W_T)
+
x(1 - T(x,W_T))
$$

## Residual Connections (ResNet)

Add input to output:

$$\Large
y = f(x,W) + x
$$

Improves gradient flow.

---

# Practical Tips

- Use differentiable operations
- Try to overfit a small batch first
- Start small, increase complexity gradually
- Match activation to task (e.g., no sigmoid for regression)
- Monitor training
- Use early stopping

Reference:
https://karpathy.github.io/2019/04/25/recipe/

---

# Summary

- CNNs: convolution, padding, strides, pooling
- Training deep nets: initialization, dropout, regularization
- Frameworks: static vs dynamic graphs
- Modern tricks: batch norm, skip connections

---

# Reading

Goodfellow et al., *Deep Learning* — Chapters 7, 8, 9, 11  

Karpathy, *A Recipe for Training Neural Networks*