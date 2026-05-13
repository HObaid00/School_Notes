# Algorithms of Scientific Computing  
## Discrete Sine Transform (DST)  
*Michael Bader, Technical University of Munich, Summer 2026* :contentReference[oaicite:0]{index=0}

---

## DFT and Symmetry

Different input symmetries lead to different Fourier-related transforms.

| Input type | Symmetry | Transform |
|---|---|---|
| real input | $f_n \in \mathbb{R}$ | Real DFT (RDFT) |
| even symmetry | $f_n = f_{-n}$ | Discrete Cosine Transform (DCT) |
| odd symmetry | $f_n = -f_{-n}$ | Discrete Sine Transform (DST) |

For “quarter-wave” input:

| Input type | Symmetry | Transform |
|---|---|---|
| even symmetry | $f_n = f_{-n-1}$ | QW-DCT |
| odd symmetry | $f_n = -f_{-n-1}$ | QW-DST |

---

## Real-Valued Input Data with Odd Symmetry

Given $2N$ input data values:

$$\Large
f_{-N+1}, \dots, f_N
$$

with all $f_n \in \mathbb{R}$ and odd symmetry:

$$\Large
f_{-n} = -f_n
$$

In particular:

$$\Large
f_0 = f_N = f_{-N} = 0
$$

For example, for $N = 4$, the data ranges from $n=-3$ to $n=4$, with zeros at $n=0$ and $n=4$.
> Reflected to make it periodic

The DFT has the form:

$$\Large
F_k =
\frac{1}{2N}
\sum_{n=-N+1}^{N}
f_n \omega_{2N}^{-nk}
$$

Using odd symmetry:

$$\Large
F_k =
\frac{1}{2N}
\sum_{n=1}^{N-1}
f_n
\left(
\omega_{2N}^{-nk}
-
\omega_{2N}^{nk}
\right)
$$

Since the difference of complex exponentials produces a sine term:

$$\Large
F_k =
-\frac{i}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(
\frac{\pi n k}{N}
\right)
$$

---

## Symmetry in the Coefficients

For odd symmetric input data, the transformed coefficients satisfy the same odd symmetry.

Starting with:

$$\Large
F_k =
-\frac{i}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(
\frac{\pi n k}{N}
\right)
$$

Then:

$$\Large
F_{-k}
=
-\frac{i}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(
\frac{\pi n(-k)}{N}
\right)
$$

Using $\sin(-x) = -\sin(x)$:

$$\Large
F_{-k}
=
-F_k
$$

Thus, the coefficient vector has the same odd symmetry. This leads to the same transform, up to scaling: the **Discrete Sine Transform**.

---

## Discrete Sine Transform (DST)

From the DFT of real-valued, odd symmetric data:

$$\Large
F_k =
-\frac{i}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(
\frac{\pi n k}{N}
\right),
\qquad
k = 1, \dots, N-1
$$

The corresponding inverse transform is:

$$\Large
f_n =
2i
\sum_{k=1}^{N-1}
F_k
\sin\left(
\frac{\pi n k}{N}
\right),
\qquad
n = 1, \dots, N-1
$$

Define:

$$\Large
\hat{F}_k := iF_k
$$

Then the DST and inverse DST are written as:

$$\Large
\hat{F}_k =
\frac{1}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(
\frac{\pi n k}{N}
\right)
$$

and

$$\Large
f_n =
2
\sum_{k=1}^{N-1}
\hat{F}_k
\sin\left(
\frac{\pi n k}{N}
\right)
$$

---

## Computation of the Discrete Sine Transform

The DST can be computed through pre-processing and post-processing around an FFT.

### Step 1: Generate a $2N$-vector with odd symmetry

For $k = 1, \dots, N-1$:

$$\Large
x_{-k} = -x_k
$$

and:

$$\Large
x_0 = x_N = 0
$$

### Step 2: Apply a fast real-valued FFT

Compute coefficients $X_k$ using a fast real-valued FFT on the vector $x$.

### Step 3: Post-process

Extract the sine transform coefficients by taking the negative imaginary part:

$$\Large
\hat{X}_k = -\operatorname{Im}\{X_k\},
\qquad
k = 1, \dots, N-1
$$

### Step 4: Scaling

Apply scaling if necessary.

---

## Recall: New Transforms and Symmetries

The DST gives a new pair of transforms:

$$\Large
F_k =
-\frac{i}{N}
\sum_{n=1}^{N-1}
f_n
\sin\left(
\frac{\pi n k}{N}
\right)
$$

and:

$$\Large
f_n =
2i
\sum_{k=1}^{N-1}
F_k
\sin\left(
\frac{\pi n k}{N}
\right)
$$

Important observations:

- Both transforms work on data sets that are neither symmetric nor periodic.
- For the particular case of the DST, we assume:
  $$\Large
  f_0 = f_N = 0
  $$
- If we extend the data according to the symmetry rules, then the reflected symmetric data becomes periodic.
- The DST is connected to the DFT and inverse DFT through a three-step procedure:

1. Extend or duplicate the data set in a symmetric way.
2. Apply the DFT or inverse DFT.
3. Extract the symmetric half of the transformed data set.

This equivalence has two important consequences:

1. A direct sine transform requires sums over $N-1$ terms for $N-1$ numbers, giving complexity:
   $$\Large
   O(N^2)
   $$

   Using an FFT reduces this to:

   $$\Large
   O(N \log N)
   $$

2. Since the DFT and inverse DFT are inverse operations on the corresponding symmetric data, the DST and inverse DST are also inverse operations.

---

## Summary: Survey on DCT/DST Variants

Different symmetry properties correspond to different ways of continuing data at the boundaries.

At the beginning and end of the data, one may choose:

| Beginning / End | even | odd |
|---|---|---|
| even | possible | possible |
| odd | possible | possible |

This gives $4$ possibilities.

Alternatively, boundary handling can be described as:

| Beginning / End | mirror | copy |
|---|---|---|
| mirror | possible | possible |
| copy | possible | possible |

This gives another $4$ possibilities.

Altogether:

$$\Large
4 \times 4 = 16
$$

So there are $16$ possible variants:

$$\Large
8 \text{ DCT variants} + 8 \text{ DST variants}
$$

---

## Summary: Common DCT/DST Schemes

Common schemes include:

- DCT-I
- DCT-II
- DCT-III
- DCT-IV
- DST-I
- DST-II
- DST-III
- DST-IV

These differ in how the signal is reflected or continued at the boundaries.

---

## Key Idea

The Discrete Sine Transform arises naturally from applying the DFT to real-valued data with odd symmetry. The odd extension causes the Fourier coefficients to be purely imaginary sine coefficients, which are then extracted and rescaled to define the DST.