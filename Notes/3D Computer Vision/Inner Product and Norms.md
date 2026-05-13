# Inner Products and Norms

## Inner Product

An inner product measures similarity between vectors.

For vectors $u$ and $v$:

$$\Large \langle u,v \rangle$$

The standard inner product in $\mathbb{R}^n$ is:

$$\Large \langle x,y \rangle = x^T y = \sum_{i=1}^n x_i y_i$$

---

## Rules

An inner product is a map $\langle \cdot , \cdot \rangle : H \times H \to \mathbb K$ satisfying:

#### Symmetry

$$\Large
\langle u , w \rangle = \langle w , u \rangle
$$

#### Linearity

$$\Large
\langle v , \alpha u \rangle = \alpha \langle v , u \rangle
$$
and

$$\Large
\langle v, u + w \rangle = \langle v, u \rangle + \langle v , w\rangle
$$

#### Positive definiteness:

$$\Large
v \not= 0 \Longrightarrow \langle v , v\rangle > 0 
$$


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

---
# Inner Product
On a vector space one can define an **inner product** (**dot product**, *Scalar*)
$$\Large  
\langle \cdot, \cdot \rangle : V \times V \to \mathbb{R}  
$$

which is defined by three properties:
1. linearity $$\Large \langle u, \alpha v + \beta w  \rangle = \alpha \langle u,v \rangle + \beta \langle u, w\rangle $$
    
2. symmetry $$\Large \langle u,v \rangle = \langle v, u\rangle $$
    
3. positive definiteness $$\Large \langle v,v \rangle \geq 0, \quad \text{and} \quad \langle v,v\rangle = 0 \iff v = 0 $$
    

The scalar product induces a norm:

$$\Large  
|\cdot |: V \rightarrow \mathbb R, \quad|v| = \sqrt{\langle v, v \rangle}  
$$

and a metric:

$$\Large  
d: V \times V \rightarrow \mathbb R, \ d(v,w) = |v-w| = \sqrt{\langle v - w , v - w \rangle}  
$$

for measuring lengths and distances, making $V$ a **metric space**. Since the metric is induced by a scalar product V is called a **Hilbert Space**

---
# Canonical and Induced Inner Product
On $V = \mathbb R ^n$, can define the canonical inner product for the canonical basis $B = I_n$ as
$$\Large  
\langle x, y \rangle = x^\top y = \sum_{i=1}^n x_i y_i  
$$
which induces the standard $L_2$-norm or Euclidean norm
$$
\Large  
|x|_2^2 = \sqrt{x^T x} = \sqrt{x_1^2+\dots + x_n^2}  
$$
With basis transform $A$ to the new basis $B'$ given by $I = B'A^{-1}$ the canonical inner product in the new coordinates $x', y'$ is given by:
$$\Large
\langle x, y \rangle= 
x^T y=
(Ax')^T(Ay') =
x'^TA^T A y' \equiv \langle x', y' \rangle_{A^T A}
$$
The latter product is called the **induced inner product** from the matrix $A$.
Two vectors $v$ and $w$ are **orthogonal iff $\langle v, w \rangle = 0$.


---
# Links
[[Hilbert Space]]
[[3D Computer Vision]]