## Dwarf #1 – Dense Linear Algebra – QR Decomposition  

Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# QR Decomposition – Problem Setting

For a matrix $A$, find $Q$ and $R$ such that:

$$
A = QR
$$

where:

- $Q$ is orthogonal:
  $$
  Q^T Q = I, \quad QQ^T = I, \quad Q^{-1} = Q^T
  $$
- $R$ is upper triangular.

---

## Motivation

- More numerically stable than Gaussian elimination / LU.
- Used for over- and underdetermined systems.

To solve $Ax = b$:

1. Compute QR factorization:
   $$
   A = QR
   $$
   Cost: $O(n^3)$
2. Multiply:
   $$
   \hat{b} = Q^T b
   $$
   Cost: $O(n^2)$
3. Solve triangular system:
   $$
   Rx = \hat{b}
   $$
   Cost: $O(n^2)$

---

# Overdetermined Systems ($m \gg n$)

Solve:

$$
\min_x \|Ax - b\|_2^2
$$

Normal equations:

$$
A^T A x = A^T b
$$

But:

$$
\mathrm{cond}(A^T A) = \mathrm{cond}(A)^2
$$

→ condition number worsens.

Using QR:

Let:

$$
A = QR, \quad
R =
\begin{pmatrix}
R_1 \\
0
\end{pmatrix}
$$

Then:

$$
R_1 x = \hat{b}_1
$$

with:

$$
\hat{b} = Q^T b =
\begin{pmatrix}
\hat{b}_1 \\
\hat{b}_2
\end{pmatrix}
$$

Advantage:

$$
\mathrm{cond}(R_1) = \mathrm{cond}(A)
$$

---

# Part I – Householder QR

## Householder Matrices

Define:

$$
H = I - \tau y y^T
$$

Properties:

- Symmetric:
  $$
  H^T = H
  $$
- Orthogonal:
  $$
  H^T H = I
  $$

Condition:

$$
2\tau = \tau^2 y^T y
$$

---

## Constructing $H_1$

Goal:

$$
H_1 a_1 = \alpha e_1
$$

Choose:

$$
\alpha = \pm \|a_1\|_2
$$

Common choice:

$$
\sigma = -\mathrm{sgn}(a_{1,1})
$$

$$
y_1 = e_1 + \frac{a_1}{\sigma \|a_1\|_2}
$$

$$
\tau_1 =
\left(
1 + \frac{a_{1,1}}{\sigma \|a_1\|_2}
\right)^{-1}
$$

---

## Recursive Procedure

After first step:

$$
H_1 A =
\begin{pmatrix}
\|a_1\|_2 & * \\
0 & A_2
\end{pmatrix}
$$

Repeat on submatrix $A_2$.

Final result:

$$
H_n \cdots H_2 H_1 A = R
$$

Thus:

$$
Q = H_1 H_2 \cdots H_n
$$

---

# Algorithm (Householder QR)

For $k = 1$ to $n$:

1. Compute $y_k$, $\tau_k$
2. Update trailing matrix:

$$
A(k:m, k+1:n)
=
(I - \tau_k y_k y_k^T)
A(k:m, k+1:n)
$$

Compact representation:

$$
Q = I - YTY^T
$$

---

# Blocked Householder QR

Partition:

$$
A =
\begin{pmatrix}
A_{11} & A_{12} \\
A_{21} & A_{22}
\end{pmatrix}
$$

Compute QR of first block column:

$$
A =
Q_1
\begin{pmatrix}
R_{11} & R_{12} \\
0 & A_{22}^{(1)}
\end{pmatrix}
$$

Compact block form:

$$
Q_k = I - Y_k T_k Y_k^T
$$

Trailing update:

$$
A = A - Y_k T_k (Y_k^T A)
$$

Uses BLAS-3 → cache efficient.

---

# Block Representation Theorem

For Householder matrices:

$$
H_k \cdots H_i
=
I - Y T_{k:i} Y^T
$$

where:

- $Y = (y_k \cdots y_i)$
- $T_{k:i}$ upper triangular

---

# Parallel QR Decomposition

Matrix distributed over $p_r \times p_c$ processors.

Issue:

Each Householder vector requires computing a column norm:

$$
\|A(k:m, k)\|_2
$$

Requires reduction across $p_r$ processors.

Latency:

$$
O(n \log p_r)
$$

---

# Communication-Avoiding QR (CAQR)

Idea:

1. Perform QR on panel (size $m \times b$).
2. Use Tall-and-Skinny QR (TSQR).
3. Apply update to trailing matrix.

---

# Tall-and-Skinny QR (TSQR)

Assume:

$$
A =
\begin{pmatrix}
A_0 \\
A_1 \\
A_2 \\
A_3
\end{pmatrix}
$$

Each processor computes:

$$
A_i = Q_i R_i
$$

Then perform tree reduction:

$$
\begin{pmatrix}
R_0 \\
R_1
\end{pmatrix}
= Q_{01} R_{01}
$$

Repeat until:

$$
R_{0123}
$$

Final factorization:

$$
A =
\begin{pmatrix}
Q_0 \\
Q_1 \\
Q_2 \\
Q_3
\end{pmatrix}
Q_{01}
Q_{0123}
R_{0123}
$$

---

## Communication Complexity

Standard QR:

$$
O(b \log p_r)
$$

TSQR:

$$
O(\log p_r)
$$

Volume unchanged:

$$
\frac{b^2}{2} \log p_r
$$

---

## FLOP Comparison

TSQR:

$$
\frac{2mn^2}{P} + \frac{2n^3}{3} \log P
$$

Standard QR:

$$
\frac{2mn^2}{P} - \frac{2n^3}{3P}
$$

Trade-off:

- Less communication
- Slightly more computation

---

# Communication-Avoiding QR (Summary)

- Use TSQR for panel factorization
- Then update trailing matrix as usual
- Achieves communication lower bounds (latency)
- Suitable for tall-skinny matrices ($m \gg n$)

---

# Literature

- Demmel et al., LAPACK Working Note 204.
- Ballard et al., *Reconstructing Householder vectors from TSQR*, 2015.
- Higham, *Accuracy and Stability of Numerical Algorithms*.
- Golub & Van Loan, *Matrix Computations*.