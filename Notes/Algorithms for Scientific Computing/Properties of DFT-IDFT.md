DFT and IDFT are (matrix-vector product) **linear**:
$$\Large
DFT(\alpha f+\beta g) = \alpha \ DFT(f) \ + \ \beta \ DFT(g)
$$
$$\Large
IDFT(\alpha f+\beta g) = \alpha \ IDFT(f) \ + \ \beta \ IDFT(g)
$$
since 
$$\Large
\omega_N^{nk} = \omega_N^{n(k+N)} = \omega_N^{(n+N)k}
$$,
the $f_n$ and the $F_k$ are **periodic:** 
$$\Large
f_{n+N} = f_n \qquad F_{k+N}=F_k \quad \text{for all } k, n \in \mathbb{Z}
$$