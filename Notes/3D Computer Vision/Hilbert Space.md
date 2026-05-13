# Hilbert Space

A **Hilbert space** is a vector space equipped with an **inner product** such that distances, lengths, and angles can be measured. In many introductory settings, especially finite-dimensional linear algebra, a Hilbert space is simply a vector space with an inner product.

## Definition

Let $(H)$ be a vector space over a field $(K)$, usually $(K=\mathbb{R})$ or $(K=\mathbb{C})$.  
An **inner product** is a function

$$\Large
\langle \cdot,\cdot\rangle : H\times H \to K
$$

that assigns two vectors $(x,y\in H)$ a scalar $(\langle x,y\rangle)$.

For a real vector space, the inner product satisfies:

1. **Symmetry**

$$\Large
\langle x,y\rangle = \langle y,x\rangle
$$

2. **Linearity in one argument**

$$\Large
\langle \lambda x+z,y\rangle
=
\lambda\langle x,y\rangle+\langle z,y\rangle
$$

3. **Positive definiteness**

$$\Large
\langle x,x\rangle \ge 0
$$

4. **Zero only for the zero vector**

$$\Large
\langle x,x\rangle = 0 \iff x=0
$$

## Induced Norm

An inner product defines a norm by

$$\Large
\|x\| = \sqrt{\langle x,x\rangle}.
$$

This norm measures the “length” of a vector.

## Example

The standard example is $(\mathbb{R}^n)$ with the dot product:

$$\Large
\langle x,y\rangle = x^T y.
$$

For

$$\Large
x=
\begin{pmatrix}
x_1\\
\vdots\\
x_n
\end{pmatrix},
\qquad
y=
\begin{pmatrix}
y_1\\
\vdots\\
y_n
\end{pmatrix},
$$

we have

$$\Large
\langle x,y\rangle
=
x_1y_1+\cdots+x_ny_n.
$$

## Intuition

A Hilbert space is a vector space where we can talk about:

- lengths of vectors,
- angles between vectors,
- orthogonality,
- projections,
- distances.

In finite dimensions, Hilbert spaces behave like familiar Euclidean spaces such as $(\mathbb{R}^2)$ and $(\mathbb{R}^3)$. 

---
# Links
[[3D Computer Vision]]