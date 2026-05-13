# 3D Computer Vision – Chapter 1

## Mathematical Background: Linear Algebra

_Prof. Dr. Daniel Cremers (TUM), Summer Term 2026_

---

## Overview

1. Vector Spaces
    
2. Linear Transformations and Matrices
    
3. Properties of Matrices
    
4. Singular Value Decomposition
    

---

## Vector Space

A set $V$ is called a vector space over $\mathbb{R}$ if it is closed under:

- vector addition: $+: V \times V \to V$
    
- scalar multiplication: $\cdot: \mathbb{R} \times V \to V$
    

such that:

- $\alpha v_1 + \beta v_2 \in V$ for all $v_1, v_2 \in V$, $\alpha, \beta \in \mathbb{R}$
    
- $(V, +)$ is a commutative group (neutral element $0$, inverse $-v$)
    
- $\alpha(\beta u) = (\alpha \beta)u$
    
- distributivity:
    
    - $(\alpha + \beta)v = \alpha v + \beta v$
        
    - $\alpha(v + u) = \alpha v + \alpha u$
        

**Example:**  
$V = \mathbb{R}^n$, $v = (x_1, \dots, x_n)^\top$

A subset $W \subset V$ is a subspace if:

- $0 \in W$
    
- closed under $+$ and scalar multiplication
    

---

## Linear Independence and Basis

Span:

$$\Large  
\text{span}(S) = \left\{ v \in V \mid v = \sum_{i=1}^k \alpha_i v_i \right\}  
$$

Linear independence:

$$\Large  
\sum_{i=1}^k \alpha_i v_i = 0 \Rightarrow \alpha_i = 0 ;\forall i  
$$

A basis $B = {v_1, \dots, v_n}$:

- linearly independent
    
- spans $V$
    

---

## Properties of a Basis

- All bases have the same number of vectors → dimension $n$
    
- Unique representation:
    

$$\Large  
v = \sum_{i=1}^n \alpha_i b_i  
$$

- Basis transformation:
    

$$\Large  
b_i' = \sum_{j=1}^n \alpha_{ji} b_j  
$$

Matrix form:

$$\Large  
B' = BA \quad \Leftrightarrow \quad B = B' A^{-1}  
$$

---

## Inner Product

$$\Large  
\langle \cdot, \cdot \rangle : V \times V \to \mathbb{R}  
$$

Properties:

1. linearity
    
2. symmetry
    
3. positive definiteness
    

Norm:

$$\Large  
|v| = \sqrt{\langle v, v \rangle}  
$$

Distance:

$$\Large  
d(v,w) = |v-w|  
$$

---

## Canonical Inner Product

$$\Large  
\langle x, y \rangle = x^\top y = \sum_{i=1}^n x_i y_i  
$$

$$\Large  
|x|_2^2 = x^\top x  
$$

Induced inner product:

$$\Large  
\langle x', y' \rangle = x'^\top A^\top A y'  
$$

Orthogonality:

$$  
\langle v, w \rangle = 0  
$$

---

## Kronecker Product

$$\Large  
A \otimes B =  
\begin{bmatrix}  
a_{11}B & \cdots & a_{1n}B \\  
\vdots & \ddots & \vdots \\  
a_{m1}B & \cdots & a_{mn}B  
\end{bmatrix}  
$$

Stack:

$$\Large  
A_s =  
\begin{bmatrix}  
a_1 \\  
\vdots \\  
a_n  
\end{bmatrix}  
$$

Identity:

$$\Large  
u^\top A v = (v \otimes u)^\top A_s  
$$

---

## Linear Transformations

A map $L: V \to W$ is linear if:

- $L(x+y) = L(x) + L(y)$
    
- $L(\alpha x) = \alpha L(x)$
    

Matrix representation:

$$\Large  
L(x) = Ax  
$$

---

## Linear Groups

General Linear Group:

$$\Large  
GL(n) = {A \in \mathcal{M}(n) \mid \det(A) \neq 0}  
$$

Special Linear Group:

$$\Large  
SL(n) = {A \mid \det(A) = 1}  
$$

---

## Affine Group

$$\Large  
L(x) = Ax + b  
$$

Homogeneous coordinates:

$$\Large  
\begin{bmatrix}  
A & b \  
0 & 1  
\end{bmatrix}  
$$

---

## Orthogonal Group

$$\Large  
O(n) = {R \mid R^\top R = I}  
$$

$$  
\det(R) \in {\pm 1}  
$$

Special orthogonal:

$$\Large  
SO(n) = O(n) \cap SL(n)  
$$

---

## Euclidean Group

$$\Large  
L(x) = Rx + T  
$$

Homogeneous form:

$$\Large  
\begin{bmatrix}  
R & T \  
0 & 1  
\end{bmatrix}  
$$

---

## Range and Null Space

$$\Large  
\text{range}(A) = {y \mid Ax = y}  
$$

$$\Large  
\ker(A) = {x \mid Ax = 0}  
$$

Solution condition:

$$  
b \in \text{range}(A)  
$$

---

## Rank

$$\Large  
\text{rank}(A) = \dim(\text{range}(A))  
$$

Key:

- $\text{rank}(A) = n - \dim(\ker(A))$
    
- $\text{rank}(A) \le \min(m,n)$
    

---

## Eigenvalues and Eigenvectors

$$\Large  
Av = \lambda v  
$$

Spectrum:

$$  
\sigma(A)  
$$

Characteristic equation:

$$\Large  
\det(\lambda I - A) = 0  
$$

---

## Symmetric Matrices

$$\Large  
S^\top = S  
$$

Diagonalization:

$$\Large  
S = V \Lambda V^\top  
$$

---

## Matrix Norms

Induced norm:

$$\Large  
|A|_2 = \max_{|x|=1} |Ax|  
$$

Frobenius:

$$\Large  
|A|_F = \sum_{i,j} a_{ij}^2 = \text{trace}(A^\top A)  
$$

---

## Skew-Symmetric Matrices

$$\Large  
A^\top = -A  
$$

Example:

$$\Large  
\hat{u} =  
\begin{bmatrix}  
0 & -u_3 & u_2 \  
u_3 & 0 & -u_1 \  
-u_2 & u_1 & 0  
\end{bmatrix}  
$$

$$  
\hat{u} v = u \times v  
$$

---

## Singular Value Decomposition (SVD)

$$\Large  
A = U \Sigma V^\top  
$$

- $U, V$ orthonormal
    
- $\Sigma = \text{diag}(\sigma_1, \dots, \sigma_p)$
    

---

## SVD Derivation

$$\Large  
A^\top A = V ,\text{diag}(\sigma_i^2), V^\top  
$$

$$\Large  
A v_i = \sigma_i u_i  
$$

Final:

$$\Large  
A = U \Sigma V^\top  
$$

---

## Geometric Interpretation of SVD

$$\Large  
y = Ax = U \Sigma V^\top x  
$$

Unit sphere → ellipsoid with axes $\sigma_i u_i$

---

## Moore–Penrose Pseudoinverse

Given:

$$\Large  
A = U \Sigma V^\top  
$$

Then:

$$\Large  
A^\dagger = V \Sigma^\dagger U^\top  
$$

where:

$$\Large  
\Sigma^\dagger =  
\begin{bmatrix}  
\Sigma_1^{-1} & 0 \  
0 & 0  
\end{bmatrix}  
$$

Properties:

$$\Large  
A A^\dagger A = A, \quad A^\dagger A A^\dagger = A^\dagger  
$$

Least-squares solution:

$$\Large  
x_{\min} = A^\dagger b  
$$

---

# Linear Algebra Wiki Notes

Source lecture: "3D Computer Vision – Ch1. Mathematical Background: Linear Algebra" by Prof. Dr. Daniel Cremers (TUM). fileciteturn0file0

---


# Vector Spaces

## Intuition

A vector space is a mathematical structure where vectors can be:

1. Added together
2. Multiplied by numbers (called scalars)

and the result always stays inside the same space.

You can think of a vector space as a "playground" where linear algebra operations behave consistently.

---

## Formal Definition

A set $V$ is called a vector space over the real numbers $\mathbb{R}$ if:

- Vector addition is defined:

$$\Large u + v \in V$$

- Scalar multiplication is defined:

$$\Large \alpha v \in V$$

for all vectors $u,v \in V$ and scalars $\alpha \in \mathbb{R}$.

The space must also satisfy rules such as:

- Associativity
- Commutativity
- Existence of a zero vector
- Existence of additive inverses
- Distributive laws

---

## Example: Euclidean Space

The most common vector space is:

$$\Large \mathbb{R}^n$$

A vector in this space looks like:

$$\Large v = (x_1, x_2, ..., x_n)^T$$

Example in $\mathbb{R}^3$:

$$\Large v = (1,2,3)^T$$

---

## Subspaces

A subset $W \subseteq V$ is called a subspace if:

1. It contains the zero vector
2. It is closed under addition
3. It is closed under scalar multiplication

Example:

All vectors of the form:

$$\Large (x,y,0)^T$$

form a plane through the origin in $\mathbb{R}^3$.

---

## Why Vector Spaces Matter

Vector spaces are the foundation of:

- Computer graphics
- Machine learning
- Robotics
- Physics
- Computer vision

Most modern numerical methods are built on vector space concepts.

---

# basis_and_linear_independence.md

```md
# Basis and Linear Independence

## Span

Given vectors:

$$\Large S = \{v_1, v_2, ..., v_k\}$$

all linear combinations form the span:

$$\Large \text{span}(S) = \left\{ \sum_{i=1}^k \alpha_i v_i \right\}$$

The span contains every vector reachable using those basis vectors.

---

## Linear Independence

Vectors are linearly independent if:

$$\Large \sum_{i=1}^k \alpha_i v_i = 0
\Rightarrow \alpha_i = 0
\quad \forall i$$

This means:

- No vector can be built from the others
- Every vector contributes unique information

### Example

The vectors:

$$\Large (1,0), (0,1)$$

are linearly independent.

But:

$$\Large (1,0), (2,0)$$

are dependent because one is a scaled version of the other.

---

## Basis

A basis is a set of vectors that:

1. Is linearly independent
2. Spans the whole space

Example basis for $\mathbb{R}^2$:

$$\Large e_1=(1,0), \quad e_2=(0,1)$$

---

## Dimension

The number of basis vectors is called the dimension.

For example:

$$\Large \dim(\mathbb{R}^3)=3$$

---

## Coordinate Representation

Every vector can be written uniquely as:

$$\Large v = \sum_{i=1}^n \alpha_i b_i$$

The coefficients $\alpha_i$ are the coordinates of the vector in that basis.

---

## Why Basis Matters

A basis provides:

- Compact representation
- Coordinate systems
- Efficient computation
- Geometric interpretation

In computer vision, changing bases often corresponds to changing camera coordinates.
```

---

# inner_products_and_norms.md

```md
# Inner Products and Norms

## Inner Product

An inner product measures similarity between vectors.

For vectors $u$ and $v$:

$$\Large \langle u,v \rangle$$

The standard inner product in $\mathbb{R}^n$ is:

$$\Large \langle x,y \rangle = x^T y = \sum_{i=1}^n x_i y_i$$

---

## Geometric Meaning

The inner product relates to angles:

$$\Large x^Ty = |x||y|\cos(\theta)$$

Therefore:

- Positive value → similar direction
- Negative value → opposite direction
- Zero → orthogonal vectors

---

## Orthogonality

Two vectors are orthogonal if:

$$\Large \langle x,y \rangle = 0$$

Orthogonality generalizes perpendicularity.

---

## Norms

A norm measures vector length.

The Euclidean norm is:

$$\Large ||x||_2 = \sqrt{x^Tx}$$

Example:

$$\Large ||(3,4)||_2 = 5$$

---

## Distance

Distance between vectors:

$$\Large d(x,y)=||x-y||$$

This is the standard geometric distance.

---

## Induced Inner Products

Changing basis can create a new inner product:

$$\Large \langle x,y \rangle_M = x^T M y$$

where:

$$\Large M = A^T A$$

This appears heavily in optimization and machine learning.

---

## Applications

Inner products are used in:

- Similarity search
- Machine learning
- Signal processing
- Projection methods
- Optimization
```

---

# linear_transformations_and_matrices.md

```md
# Linear Transformations and Matrices

## Linear Transformations

A linear transformation maps vectors to vectors while preserving:

1. Addition
2. Scalar multiplication

Formally:

$$\Large L(x+y)=L(x)+L(y)$$

$$\Large L(\alpha x)=\alpha L(x)$$

---

## Matrix Representation

Every linear transformation can be represented by a matrix:

$$\Large L(x)=Ax$$

where:

$$\Large A \in \mathbb{R}^{m\times n}$$

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
```

---

# matrix_groups.md

```md
# Matrix Groups

## What is a Group?

A group is a set equipped with an operation satisfying:

1. Closure
2. Associativity
3. Identity element
4. Inverse element

---

## General Linear Group

The set of invertible matrices forms:

$$\Large GL(n)$$

A matrix belongs to $GL(n)$ if:

$$\Large \det(A) \neq 0$$

Such matrices have inverses.

---

## Special Linear Group

Matrices with determinant 1 form:

$$\Large SL(n)$$

These preserve oriented volume.

---

## Orthogonal Group

Orthogonal matrices satisfy:

$$\Large R^TR = I$$

These preserve:

- Lengths
- Angles
- Inner products

Their inverse equals their transpose:

$$\Large R^{-1}=R^T$$

---

## Special Orthogonal Group

Rotation matrices belong to:

$$\Large SO(n)$$

where:

$$\Large \det(R)=1$$

In 3D graphics and robotics:

$$\Large SO(3)$$

represents all 3D rotations.

---

## Affine Transformations

Affine transformations combine:

- Linear transformation
- Translation

Formula:

$$\Large L(x)=Ax+b$$

---

## Euclidean Group

Rigid-body motions are:

$$\Large x \mapsto Rx + T$$

with:

$$\Large R \in SO(n)$$

These preserve distances.

---

## Applications

Matrix groups are essential in:

- Robotics
- Camera motion
- 3D graphics
- Physics
- Pose estimation
```

---

# range_kernel_and_rank.md

```md
# Range, Kernel, and Rank

## Range

The range of a matrix contains all vectors reachable by:

$$\Large y = Ax$$

Formally:

$$\Large \text{range}(A)=\{y\mid \exists x: Ax=y\}$$

The range equals the span of the matrix columns.

---

## Kernel (Null Space)

The kernel contains all vectors mapped to zero:

$$\Large \ker(A)=\{x\mid Ax=0\}$$

These vectors disappear under the transformation.

---

## Solving Linear Systems

The equation:

$$\Large Ax=b$$

has a solution only if:

$$\Large b \in \text{range}(A)$$

---

## Uniqueness

Solutions are unique only if:

$$\Large \ker(A)=\{0\}$$

Otherwise infinitely many solutions exist.

---

## Rank

The rank measures the dimension of the range:

$$\Large \text{rank}(A)=\dim(\text{range}(A))$$

---

## Rank-Nullity Theorem

One of the most important results:

$$\Large \text{rank}(A)+\dim(\ker(A))=n$$

where $n$ is the number of columns.

---

## Interpretation

- High rank → more information preserved
- Low rank → compression or degeneracy

---

## Applications

Rank is central in:

- Data compression
- Least squares
- Machine learning
- Computer vision
- PCA
```

---

# eigenvalues_and_eigenvectors.md

```md
# Eigenvalues and Eigenvectors

## Core Idea

An eigenvector keeps its direction after transformation.

If:

$$\Large Av = \lambda v$$

then:

- $v$ is an eigenvector
- $\lambda$ is the eigenvalue

---

## Interpretation

The matrix transforms the vector only by scaling.

- $|\lambda|>1$ → stretching
- $|\lambda|<1$ → shrinking
- Negative $\lambda$ → direction flip

---

## Characteristic Equation

Eigenvalues satisfy:

$$\Large \det(\lambda I - A)=0$$

This polynomial is called the characteristic polynomial.

---

## Symmetric Matrices

Symmetric matrices have special properties:

1. Real eigenvalues
2. Orthogonal eigenvectors
3. Orthogonal diagonalization

---

## Diagonalization

A symmetric matrix can be written as:

$$\Large A = V\Lambda V^T$$

where:

- $V$ contains eigenvectors
- $\Lambda$ contains eigenvalues

---

## Why Eigenvalues Matter

Eigenanalysis is used in:

- PCA
- Stability analysis
- Quantum mechanics
- Vibrations
- Spectral graph theory
- Machine learning
```

---

# matrix_norms.md

```md
# Matrix Norms

## Purpose of Matrix Norms

Matrix norms measure the "size" or "strength" of a matrix.

---

## Induced 2-Norm

The induced norm measures maximum stretching:

$$\Large ||A||_2 = \max_{||x||_2=1} ||Ax||_2$$

This equals the largest singular value:

$$\Large ||A||_2 = \sigma_1$$

---

## Frobenius Norm

The Frobenius norm sums all squared entries:

$$\Large ||A||_F = \sqrt{\sum_{i,j} a_{ij}^2}$$

Equivalent form:

$$\Large ||A||_F = \sqrt{\text{trace}(A^TA)}$$

---

## Interpretation

- Spectral norm → maximum amplification
- Frobenius norm → total energy

---

## Applications

Matrix norms appear in:

- Optimization
- Numerical analysis
- Machine learning
- Error estimation
- Regularization
```

---

# skew_symmetric_matrices.md

```md
# Skew-Symmetric Matrices

## Definition

A matrix is skew-symmetric if:

$$\Large A^T = -A$$

This means:

- Diagonal entries are zero
- Upper triangle is negative lower triangle

---

## 3D Cross Product Matrix

For:

$$\Large u=(u_1,u_2,u_3)^T$$

its hat matrix is:

$$\Large
\hat{u}=
\begin{bmatrix}
0 & -u_3 & u_2 \\
u_3 & 0 & -u_1 \\
-u_2 & u_1 & 0
\end{bmatrix}
$$

---

## Cross Product Representation

The hat matrix satisfies:

$$\Large \hat{u}v = u \times v$$

This converts cross products into matrix multiplication.

---

## Properties

Skew-symmetric matrices:

- Have purely imaginary eigenvalues
- Have even rank
- Represent rotations infinitesimally

---

## Applications

They are heavily used in:

- Robotics
- Rigid-body motion
- Lie groups
- Computer vision
- Rotational dynamics
```

---

# singular_value_decomposition.md

```md
# Singular Value Decomposition (SVD)

## What is SVD?

The Singular Value Decomposition factorizes a matrix into:

$$\Large A = U\Sigma V^T$$

where:

- $U$ contains left singular vectors
- $V$ contains right singular vectors
- $\Sigma$ contains singular values

---

## Why SVD Matters

SVD is one of the most important tools in linear algebra.

It works for:

- Square matrices
- Rectangular matrices
- Rank-deficient matrices

---

## Geometric Interpretation

SVD transforms space in three stages:

1. Rotate using $V^T$
2. Scale using $\Sigma$
3. Rotate using $U$

The unit sphere becomes an ellipsoid.

The singular values determine the axis lengths.

---

## Singular Values

Singular values are:

$$\Large \sigma_i = \sqrt{\lambda_i(A^TA)}$$

where $\lambda_i$ are eigenvalues.

---

## Rank and SVD

The number of nonzero singular values equals:

$$\Large \text{rank}(A)$$

---

## Applications

SVD is used in:

- PCA
- Image compression
- Noise reduction
- Least squares
- Recommendation systems
- Computer vision

---

## Low-Rank Approximation

Keeping only the largest singular values produces a compressed approximation:

$$\Large A \approx U_k \Sigma_k V_k^T$$

This is foundational in data compression.
```

---

# pseudoinverse.md

```md
# Moore-Penrose Pseudoinverse

## Motivation

Not all matrices are invertible.

- Some are rectangular
- Some are singular

The pseudoinverse generalizes matrix inversion.

---

## Definition

If:

$$\Large A = U\Sigma V^T$$

then the pseudoinverse is:

$$\Large A^\dagger = V\Sigma^\dagger U^T$$

where:

$$\Large \Sigma^\dagger$$

contains reciprocals of nonzero singular values.

---

## Solving Linear Systems

For:

$$\Large Ax=b$$

one solution is:

$$\Large x=A^\dagger b$$

---

## Least-Squares Interpretation

The pseudoinverse finds:

1. The least-squares solution
2. The minimum-norm solution

This is extremely important when systems are overdetermined.

---

## Applications

The pseudoinverse is used in:

- Linear regression
- Optimization
- Robotics
- Signal processing
- Neural networks
- Computer vision
```