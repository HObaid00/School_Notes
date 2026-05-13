# Loss Function - Least Square

Now, how do we choose the "best" $\omega$ that fits our data?

A **loss function** measures the "misfit" or error between our model (parameterized by $\omega$) and observed data $D = \{(x_i, \ y_i)\}_{i=1}^N$.

Standard choice - **[[Minsta Kvadrat Metoden (MK)]] / Least Square (LS)** 
$$\Large
E_{LS} = 
\frac 1 2 \sum_{i=1}^{N}(f_w(x_i) - y_i)^2
$$

Matrix form:
$$
\Large 
E_{LS} = \frac 1 2 \sum_{i=1}^N (\omega^T x_i - y_i)^2
$$

---
# Objective

The objective of any Linear Regression problem is to find the optimal weighted vector $\omega^*$ that minimizes the error
$$\Large
w^* = \arg\min_w E_{LS}(\mathbb{\omega}) = 
\arg\min_\omega (x_i^T \omega - y_i)^2
$$
By stacking the observation $x_i$ as rows of the matrix $X \in \mathbb{R}^{N \times D}$ 
$$\Large
= \arg\min \frac 1 2 (X\omega - y)^T(X\omega - y)
$$
---
# Optimal Solution

To find the minimum of the loss $E(\omega)$, compute the [[Gradient]] $\nabla_\omega E(\omega)$:
$$\Large
\begin{array}a
\nabla_w E_{LS}(w) = \nabla_w \frac 12(Xw - y)^T(Xw - y)\\
= \nabla_w \frac 12(w^T X^T X w - 2 w^T X^T y + y^T y) \\
= X^T X w - X^T y
\end{array}
$$
Meaning we derive the function $E_{LS}$. Then we set it to zero:
$$\Large
X^TXw - X^T y = 0
$$
which leads to the **normal equation** of the least squares problem:
$$\Large
w^* =
\underbrace{(X^T X)^{-1} X^T}_{X^\dagger} y
=
X^\dagger y
$$
Where $X^\dagger$ is called the **[[Moore-Penrose Pseudo Inverse]]**   

---
# Links
[[Machine Learning]]
[[Minsta Kvadrat Metoden (MK)]]
[[Moore-Penrose Pseudo Inverse]]
[[Gradient]]