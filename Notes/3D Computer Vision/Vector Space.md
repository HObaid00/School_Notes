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

  

- Vector addition is defined as if two vectors are added together then :

  

$$\Large u + v \in V$$

  

- Scalar multiplication is defined:

  

$$\Large \alpha v \in V$$

  

for all vectors $u,v \in V$ and scalars $\alpha \in \mathbb{R}$.

  

The space must also satisfy rules such as:

  

- Associativity $$\Large (a \cdot b) \cdot c = a \cdot (b \cdot c) $$

- Commutativity $$\Large a \cdot b = b \cdot a$$

- Existence of a zero vector $$\Large \bar 0 = \{0, \dots , 0\} $$

- Existence of additive inverses $$\Large u + (-u) = 0 $$

- Distributive laws$$\Large \alpha(x + y) = \alpha x + \alpha y $$

  

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

  

1. It contains the zero vector $$\Large \bar 0  = \{0_1, 0_2, \dots, 0_n\}$$

2. It is closed under addition $$\Large u, v \in W, \quad u + v \in W $$

3. It is closed under scalar multiplication $$\Large v \in V, \quad \alpha v \in V $$

  

### Example:
  

All vectors of the form:

  

$$\Large (x,y,0)^T$$

  

form a plane through the origin in $\mathbb{R}^3$.

  

---

  

## Why Vector Spaces Matter

  

Vector spaces are the foundation of:

  

- Computer graphics

Most modern numerical methods are built on vector space concepts.

---
# Links
[[3D Computer Vision]]
[[Linear Algebra]]

