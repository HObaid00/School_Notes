# Matrix Groups

## What is a Group?

A group is a set equipped with an operation satisfying:

1. Closure$$\Large g_1 \circ g_2 \in G \quad \forall g_1 g_2 \in G$$
2. Associativity$$\Large (g_1 \circ g_2) \circ g_3 = g_1 \circ (g_2 \circ g_3) \quad \forall g_1, g_2, g_3 \in G$$
3. Identity element $$\Large \exists e \in G: e \circ g = g \circ e = g \quad \forall g \in G $$
4. Inverse element $$\Large \exists g^{-1} \in G: g \circ g^{-1} = g^{-1} \circ g = e \quad \forall g \in G $$

---

## General Linear Group

The set of invertible matrices forms:

$$\Large GL(n) = {A \in \mathcal{M}(n)}$$

A matrix belongs to $GL(n)$ if:

$$\Large \det(A) \neq 0$$

Such matrices have inverses.

---

## Special Linear Group

Matrices with determinant 1 form:

$$\Large SL(n) = A \mid \det(A)=1$$

These preserve oriented volume.

---
## Inverse of $A$
$$\Large
det(A^{-1}) = det(A)^{-1}$$

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

The set of all such affine transformations is called the **affine group of dimension** $n$, denoted by $A(n)$.
$L$ defined above is not a linear map unless $b = 0$. By introducing **homogeneous coordinates** to represent $x \in \mathbb R ^n$ by $\begin{pmatrix} x \\ 1 \end{pmatrix} \in \mathbb R^{n+1}, \ L$ becomes a linear mapping from    
$$\Large  
L : \mathbb R^{n+1} \to \mathbb R^{n+1}; \quad 
\begin{pmatrix}
x \\ 1
\end{pmatrix}
\mapsto
\begin{pmatrix}  
A & b \\  
0 & 1  
\end{pmatrix}  
\begin{pmatrix}
x \\ 1
\end{pmatrix}
$$
A matrix $\begin{pmatrix} A & b \\ 0 & 1\end{pmatrix}$ with $A \in GL(n)$ and $b \in \mathbb R^n$ is called an affine matrix. It is an element of $GL(n+1)$. The affine matrices form a subgroup of $GL(n+1)$. 

Why? see **Orthogonal Group**

---

## Euclidean Group
A Euclidean transformation $L$ from $\mathbb R^n$ to $\mathbb R^n$ is defined by an orthogonal matrix $R \in O(n)$ and a vector $T \in \mathbb R^n$:
Rigid-body motions are:

$$\Large L: \mathbb R^n \to \mathbb R^n;\quad x \mapsto Rx + T$$

with:

$$\Large R \in SO(n)$$

These preserve distances.

The set of all such transformations is called the **Euclidean group** $E(n)$. It is a subgroup of the affine group $A(n)$. Embedded by homogeneous coordinates, we get:  

$$\Large
E(n) = \{
\begin{pmatrix}  
R & T \\  
0 & 1  
\end{pmatrix}
\mid  R \in O(n), T \in \mathbb R^n
\}
$$
If $R \in SO(n)$ (i.e. $det(R)= 1$), then we have the **special Euclidean group** $SE(n)$. In particular, $SE(3)$ represents the **rigid-body motions** in $\mathbb R^3$.

### Summery
$$\Large
SO(n) \subset O(n) \subset GL(n), \quad SE(n) \subset E(n) \subset A(n) \subset GL(n+1)
$$
Where $x \subset y$ means x is a subset of y.


---

## Applications

Matrix groups are essential in:

- Robotics
- Camera motion
- 3D graphics
- Physics
- Pose estimation

---
# Links
[[3D Computer Vision]]