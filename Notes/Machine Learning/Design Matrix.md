
## Definition
For *d*-dimensional data $x: \quad \phi_j: \mathbb R ^d \rightarrow \mathbb R$  

Prediction for one sample then becomes:
$$\Large
f_w(x) = w_0 + \sum_{j=1}^M
w_j \phi_j (x) = w^T \phi(x)
$$

Using Least Square error function ([[Minsta Kvadrat Metoden (MK)]]):
$$\Large
E_{LS} = \frac 12 \sum^N(w^T\phi(x_i) - y_i )^2 = \frac 12 (\Phi w - y)^T
(\Phi w - y)
$$

with 
$$\Large
\Phi = 
\begin{pmatrix}
\phi_0(x_1) & \phi_1(x_1) & \dots & \phi_M(x_1) \\
\phi_0(x_2) & \phi_1(x_2) & \dots & \phi_M(x_2) \\
\vdots & \vdots & \ddots & \vdots \\
\phi_0(x_N) & \phi_1(x_N) & \dots & \phi_M(x_N) 
\end{pmatrix}

\in \mathbb R ^{N \times (M+1)}
$$

begin the **design matrix** of $\mathbb{\phi}$.

---
# Interpretation

- rows = data points
- columns = transformed features

---

# Prediction Formula

Predictions become:

$$\Large
f_w(x)=w^T\phi(x)
$$

---

# Least Squares with Basis Functions

The loss becomes:

$$\Large
E_{LS}(w)
=
\frac12
(\Phi w-y)^T(\Phi w-y)
$$

---

# Closed-Form Solution

The optimal weights are:

$$\Large
w^*
=
(\Phi^T\Phi)^{-1}\Phi^Ty = \Phi^\dagger y
$$

Exactly the same structure as ordinary linear regression.

---
# Links
[[Basis functions]]
[[Least Square Loss]]
[[Moore-Penrose Pseudo Inverse]]
[[Machine Learning]]
