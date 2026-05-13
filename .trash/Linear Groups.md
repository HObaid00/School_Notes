## Linear Groups
There exist certain sets of linear transformations which form a group. A **group** is a set G with an operation $\circ$: $G \times G \to G$ such that :

1.  closed: $$\Large g_1 \circ g_2 \in G \ \forall g_1 g_2 \in G$$ 
2. associated: $$\Large (g_1 \circ g_2) \circ g_3 = g_1 \circ (g_2 \circ g_3) \ \forall g_1, g_2, g_3 \in G$$
3. neutral: $$\Large \exists e \in G: e \circ g = g \circ e = g \quad \forall g \in G $$
4. inverse: $$\Large \exists g^{-1} \in G: g \circ g^{-1} = g^{-1} \circ g = e \quad \forall g \in G $$
---
# Example
All invertible (non-singular) real $n \times n$-matrices form a group with respect to matrix multiplication. This group is called the **general linear group** $GL(n)$. It consists of all $A \in \mathcal M (n)$ for which all matrices in the **General Linear Group**:

$$\Large  
GL(n) = {A \in \mathcal{M}(n) \mid \det(A) \neq 0}  
$$

In **Special Linear Group**:

$$\Large  
SL(n) = {A \mid \det(A) = 1}  
$$
The inverse of $A$ is also in this group, as 
$$\Large
det(A^{-1}) = det(A)^{-1}
$$

---
# Matrix Representation of Groups
A group $G$ has a **matrix representation** or can be realized as a matrix group if there exists an injective transformations:
$$\Large
R: G \to GL(n)
$$
which **preserved the group structure** of $G$, that is inverse and composition are preserved by the map:
$$\Large
R(e) = I_{n\times n}, \quad R(g \circ h) = R(g)R(h) \ \forall g, h \in G
$$
Such a map $R$ is called **group homomorphism**. The idea of matrix representations of a group is that they allow to analyze more abstract groups by looking at the properties of the respective matrix group.

**Example:** The rotations of an object form a group, as there exists a neutral element (no rotation) and an inverse (the inverse rotation) and any concatenation of rotations is again a rotation (around a different axis). Studying the properties of the rotation group is easier if rotation are represented by respective matrices.

---
# Links
[[3D Computer Vision]]