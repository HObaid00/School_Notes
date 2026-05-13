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

---
# Links
[[Linear Algebra]]
[[3D Computer Vision]]