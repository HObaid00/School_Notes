## Kronecker Product
Given two matrices $A \in \mathbb R ^{m \times n}$ and $B \in \mathbb R ^{k \times l}$, one can define their **Kronecker product**:
$$\Large  
A \otimes B =  
\begin{bmatrix}  
a_{11}B & \cdots & a_{1n}B \\  
\vdots & \ddots & \vdots \\  
a_{m1}B & \cdots & a_{mn}B  
\end{bmatrix}  
$$

Given a matrix $A \in \mathbb R ^{m \times n}$, its **stack** $A_s$ is obtained by stacking its $n$ column vectors $a_1, \dots, a_n \in \mathbb R^m$:

$$\Large  
A_s =  
\begin{bmatrix}  
a_1 \\  
\vdots \\  
a_n  
\end{bmatrix}  
\in \mathbb R ^{mn}
$$

These notations allow to rewrite algebraic expressions, for example Identity:

$$\Large  
u^\top A v = (v \otimes u)^\top A_s  
$$

---
# Links
[[3D Computer Vision]]