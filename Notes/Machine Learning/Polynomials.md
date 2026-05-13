# Polynomials
in some functions the data doesn't follow a linear line instead i might be aligned some $\sin$ function. 

![[Pasted image 20260504103558.png]]


Example data:

$$\Large
y_i = \sin(2\pi x_i) + \epsilon_i
$$

---
# Key Idea
Transform the input using basis functions. 
$$\Large f_w(x)=w_0+w_1x $$
Then use polynomials as the universal function appropriators, so for 1-dimensional $x$ we can define $f$ as:

$$\Large
f_w(x) =
w_0 + \sum_{j=1}^M w_j x^j
$$

more generally

$$\Large
f_w(x) = w_0 + \sum_{j=1}^M w_j \phi_j(x) =
w^T \phi(x)
$$

As shown in [[Absorbing the Bias]] we absorb $w_0$ by adding a $\phi_0 = 1$.
Then the function has become linear regarding in $w$, but nonlinear in $x$.

---
[[Machine Learning]]
[[Absorbing the Bias]]
[[Basis functions]]

