
$$\Large
X=(X_1,\dots,X_r)\in MN(\mu,\Sigma)
$$

där

- $\mu\in\mathbb{R}^r$
- $\Sigma$ kovariansmatris

---

### Täthetsfunktion

$$\Large
f(x)=
((2\pi)^n \det\Sigma)^{-1}
e^{-\frac12(x-\mu)\Sigma^{-1}(x-\mu)^T}
$$

---

### Sats

Om

$$\Large
(X,Y)\in MN
\left(
\begin{bmatrix}\mu_X\\\mu_Y\end{bmatrix},
\begin{bmatrix}c_{11}&c_{12}\\c_{21}&c_{22}\end{bmatrix}
\right)
$$

så gäller

$$\Large
X|Y=y \in
N\left(
\mu_X+\frac{c_{12}}{c_{22}}(y-\mu_Y),
c_{11}-\frac{c_{12}^2}{c_{22}}
\right)
$$

---
