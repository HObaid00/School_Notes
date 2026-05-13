# Algorithms of Scientific Computing  
## Quarter-Wave DFT and Discrete Cosine Transform (QW-DCT)

**Michael Bader – TU Munich (Summer 2026)**

---

## Fast Fourier Transform – Outline

- Discrete Fourier Transform (DFT)  
- Fast Fourier Transform (FFT)  
- Special Fourier Transforms:
  - Real-valued FFT  
  - Sine/Cosine Transform  
- Applications:
  - Fast Poisson Solver  
  - Computer Graphics  
- Efficient Implementation  

---

## Motivation: Image Compression (JPEG)

Compression pipeline:

1. Color space conversion (e.g., YCbCr)  
2. Downsampling (color components)  
3. Blockwise **Quarter-Wave DCT (8×8 blocks)**  
4. Quantization  
5. Entropy coding (Huffman / arithmetic)

➡️ Insert figure: JPEG pipeline diagram

---

## Discrete Fourier Transform (DFT)

$$\Large F_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n e^{-i2\pi nk/N}$$

Interpretation:

- Trigonometric interpolation  
- Approximation of Fourier series coefficients  

---

## Fourier Series

$$\Large f(x) \sim \sum_{k=-\infty}^{\infty} c_k e^{ikx}$$

$$\Large c_k = \frac{1}{2\pi} \int_0^{2\pi} f(x)e^{-ikx}\,dx$$

---

## Orthogonality

$$\Large \langle f, g \rangle = \frac{1}{2\pi} \int_0^{2\pi} f(x)^* g(x)\,dx$$

$$\Large 
\frac{1}{2\pi}\int_0^{2\pi} e^{ikx}e^{-inx}dx =
\begin{cases}
1 & k=n \\
0 & k \ne n
\end{cases}
$$

---

## Trapezoidal Approximation → DFT

$$\Large c_k \approx \frac{1}{N} \left(\frac{f_0}{2} + \sum_{n=1}^{N-1} f_n e^{-i2\pi nk/N} + \frac{f_N}{2}\right)$$

For periodic data:

$$\Large F_k = \frac{1}{N}\sum_{n=0}^{N-1} f_n e^{-i2\pi nk/N}$$

---

## Midpoint Rule → Quarter-Wave DFT

$$\Large \tilde{F}_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n e^{-i2\pi (n+\frac{1}{2})k/N}$$

---

## Quarter-Wave DFT

Forward:

$$\Large \tilde{F}_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n e^{-i2\pi (n+\frac{1}{2})k/N}$$

Inverse:

$$\Large f_n = \sum_{k=0}^{N-1} \tilde{F}_k e^{i2\pi (n+\frac{1}{2})k/N}$$

Relation:

$$\Large F_k = \tilde{F}_k e^{i\pi k/N}$$

➡️ Insert figure: midpoint sampling vs standard grid

---

## Symmetry → Cosine Transform

For symmetric data:

$$\Large \tilde{F}_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)$$

---

## Quarter-Wave DCT (QW-DCT)

Forward:

$$\Large \tilde{F}_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)$$

Inverse:

$$\Large f_n = \tilde{F}_0 + 2 \sum_{k=1}^{N-1} \tilde{F}_k \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)$$

---

## Properties

- Real-valued transform  
- Works for non-periodic data  
- Efficient via FFT: $\Large O(N \log N)$  

---

## 2D QW-DCT (JPEG)

$$\Large \tilde{F}_{kl} =
\frac{1}{NM} \sum_{n=0}^{N-1}\sum_{m=0}^{M-1}
f_{nm}
\cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)
\cos\left(\frac{\pi l (m+\frac{1}{2})}{M}\right)$$

$$\Large f_{nm} =
4 \sum_{k=0}^{N-1} \sum_{l=0}^{M-1}
\tilde{F}_{kl}
\cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)
\cos\left(\frac{\pi l (m+\frac{1}{2})}{M}\right)$$

➡️ Insert figure: 8×8 DCT block visualization

---

## Separability (2D → 1D)

1. Transform rows  
2. Transform columns  

---

## Algorithm

Row transform:

$$\Large \tilde{F}_{nl} = \frac{1}{N} \sum_{m=0}^{N-1} f_{nm} \cos\left(\frac{\pi l (m+\frac{1}{2})}{N}\right)$$

Column transform:

$$\Large \tilde{F}_{kl} = \frac{1}{N} \sum_{n=0}^{N-1} \tilde{F}_{nl} \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)$$

---

## JPEG Application

- Blockwise 2D QW-DCT  
- Quantization  
- Entropy coding  

➡️ Insert figure: DCT coefficient heatmap

---

## Fast QW-DCT

$$\Large \tilde{F}_k = G_k e^{-i\pi k / 2N}$$

- Naive: $\Large O(N^2)$  
- FFT-based: $\Large O(N \log N)$  

---

## Summary

- QW-DCT comes from midpoint sampling  
- Produces cosine-only transform  
- Core tool in JPEG compression  
- Efficient via FFT  