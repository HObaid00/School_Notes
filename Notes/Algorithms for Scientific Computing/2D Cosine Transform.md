# Definition


$$\Large \tilde{F}_{kl} =
\frac{1}{NM} \sum_{n=0}^{N-1}\sum_{m=0}^{M-1}
f_{nm}
\cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)
\cos\left(\frac{\pi l (m+\frac{1}{2})}{M}\right)
$$

$$\Large f_{nm} =
4 \sum_{k=0}^{N-1} \sum_{l=0}^{M-1}
\tilde{F}_{kl}
\cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)
\cos\left(\frac{\pi l (m+\frac{1}{2})}{M}\right)$$
Where $\Large k \ \& \ l$ are the frequency components

shortened notation:
$$\Large
\sum_{k=0}^{N-1}x_k := \frac{x_0}{2} + \sum_{k=1}^{N-1}x_k 
$$
---
# Reducing 2D to 1D Transforms
In the 2D transform, we can rearrange:
$$
\Large \tilde{F}_{kl} =
\frac{1}{N} \sum_{n=0}^{N-1}
\underbrace{

\left( \frac 1 N \sum_{m=0}^{M-1}
f_{nm}
\cos\left(\frac{\pi k (m+\frac{1}{2})}{M}\right)
\right)

}
_{:= \hat{F}_{nl}}
\cos\left(\frac{\pi l (m+\frac{1}{2})}{M}\right)

$$
* For each $\Large n, \hat{F}_{nl}$ are computed via *N* 1D transforms
* we may first 1D-transform all rows and then all columns to get the 2D-transform

---
# 2D Quarter Wave Fast Cosine Transform (QW-FCT) Algorithm
1. Apply a 1D QW-FCT for att $\Large n= 0, \dots, N-1$: $$\Large \hat{F}_{nl} = \frac{1}{M} \sum_{m=0}^{M-1} f_{nm} \cos\left(\frac{\pi l (m+\frac{1}{2})}{M}\right) $$ (transform all "rows").
2. Apply a 1D QW-FCT for all $\Large l = 0, \dots, N-1$: $$\Large \hat{F}_{nl} = \frac{1}{N} \sum_{n=0}^{N-1} F_{nl} \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right) $$ (transform all "columns").

---
