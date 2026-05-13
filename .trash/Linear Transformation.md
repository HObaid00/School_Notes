## Linear Transformations
A **linear transformation** $L$ between two linear spaces $V$ and $W$ is a map $L: V \to W$ is linear if:

- $L(x+y) = L(x) + L(y)$
    
- $L(\alpha x) = \alpha L(x)$
    

Due to the linearity, the action of $L$ on the space $V$ is uniquely defined by its action on the basis vectors of $V$. On the canonical basis $\{e_1, \dots, e_n\}$ we have:
Matrix representation:

$$\Large  
L(x) = Ax\quad \forall x \in V,
$$
Where
$$\Large
A = (L(e_1), \dots, L(e_n)) \in \mathbb R ^{m\times n}
$$
The set of all real $m \times n$ matrices is denoted by $\mathcal{M}(m,n)$. In the case that $m=n$, the set  $\mathcal M (m,n) \equiv \mathcal M (n)$ forms a **ring** over the field $\mathbb{R}$, i..e. it is closed under matrix multiplication and summation.

---
# Links
[[3D Computer Vision]]