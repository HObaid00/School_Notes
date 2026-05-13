## Definition
A matrix $A \in \mathcal M (n)$ is called **orthogonal** if it preserves the inner product, i.e.:
$$\Large
\langle Ax, Ay\rangle = \langle x, y \rangle, \quad \forall x, y \in \mathbb R^n.
$$
The set of all orthogonal matrices forms the orthogonal group $O(n)$, which is a subgroup of $GL(n)$. For an orthogonal matrix R we have
$$\Large
\langle Rx, Ry \rangle = x^T R^T R y = x^T y, \quad \forall x,y \in \mathbb R^n
$$
Therefor we must have $R^T R = RR^T$, in other words:
$$\Large  
O(n) = \{R \in GL(n) \mid R^\top R = I\},  
$$
The above identity shows that for any orthogonal matrix R, we have $det(R^T R) = (det(R))^2 = det(I) = 1$, such that $det(R) \in \{± 1\}$. 

The subgroup of $O(n)$ with $det(R) = +1$ is called the **special orthogonal group** $SO(n)$. 

$$\Large  
SO(n) = O(n) \cap SL(n)  
$$
In particular, $SO(3)$ is the group of all 3-dimensional **rotation matrices**

---
## Links
[[3D Computer Vision]]
