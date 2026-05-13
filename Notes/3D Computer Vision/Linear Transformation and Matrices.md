# Linear Transformations and Matrices

## Linear Transformations

A linear transformation maps vectors to vectors while preserving:

1. Addition
2. Scalar multiplication

Formally:

$$\Large L(x+y)=L(x)+L(y)$$

$$\Large L(\alpha x)=\alpha L(x)$$

Due to the linearity, the action of $L$ on the space $V$ is uniquely defined by its action on the basis vectors of $V$. On the canonical basis $\{e_1, \dots, e_n\}$ we have:
$$\Large  
L(x) = Ax\quad \forall x \in V,$$
Where
$$\Large
A = (L(e_1), \dots, L(e_n)) \in \mathbb R ^{m\times n}$$


---

## Matrix Representation

Every linear transformation can be represented by a matrix:

$$\Large L(x)=Ax$$

where:

$$\Large A \in \mathbb{R}^{m\times n}$$
The set of all real $m \times n$ matrices is denoted by $\mathcal{M}(m,n)$. In the case that $m=n$, the set  $\mathcal M (m,n) \equiv \mathcal M (n)$ forms a **ring** over the field $\mathbb{R}$, i..e. it is closed under matrix multiplication and summation.

---

## Geometric Interpretation

Matrices can:

- Rotate
- Scale
- Reflect
- Shear
- Project

vectors.

---

## Basis Action

A matrix is fully determined by what it does to basis vectors.

If:

$$\Large A=[Ae_1\; Ae_2\; ...\; Ae_n]$$

then the columns of $A$ describe transformed basis vectors.

---

## Matrix Multiplication

Applying two transformations sequentially:

$$\Large y = BAx$$

means:

1. Apply $A$
2. Then apply $B$

---

## Why Linear Transformations Matter

They are fundamental in:

- Computer graphics
- Neural networks
- Robotics
- Physics
- Control systems

---
# Links
[[3D Computer Vision]]
