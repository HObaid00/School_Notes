## Definition
An affine transformation $L: \mathbb R^n \to \mathbb R^n$ is defined by a matrix $A \in GL(n)$ and a vector $b \in \mathbb R ^n$ such that
$$\Large  
L(x) = Ax + b  
$$
The set of all such affine transformations is called the **affine group of dimension** $n$, denoted by $A(n)$.
$L$ defined above is not a linear map unless $b = 0$. By introducing **homogeneous coordinates** to represent $x \in \mathbb R ^n$ by $\begin{pmatrix} x \\ 1 \end{pmatrix} \in \mathbb R^{n+1}, \ L$ becomes a linear mapping from    
$$\Large  
L : \mathbb R^{n+1} \to \mathbb R^{n+1}; \quad 
\begin{pmatrix}
x \\ 1
\end{pmatrix}
\to
\begin{pmatrix}  
A & b \\  
0 & 1  
\end{pmatrix}  
\begin{pmatrix}
x \\ 1
\end{pmatrix}
$$
A matrix $\begin{pmatrix} A & b \\ 0 & 1\end{pmatrix}$ with $A \in GL(n)$ and $b \in \mathbb R^n$ is called an affine matrix. It is an element of $GL(n+1)$. The affine matrices form a subgroup of $GL(n+1)$. 

Why? see [[Orthogonal Group]]

---
# Links
[[Linear Groups]]
[[Orthogonal Group]]
[[3D Computer Vision]]