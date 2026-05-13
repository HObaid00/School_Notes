# Definition
New pair of transformers:

Forward:

$$\Large \tilde{F}_k := \frac{1}{N} \sum_{n=0}^{N-1} f_n e^{-i2\pi (n+\frac{1}{2})k/N}$$

Inverse:

$$\Large f_n := \sum_{k=0}^{N-1} \tilde{F}_k e^{i2\pi (n+\frac{1}{2})k/N}$$

Relation:

$$\Large F_k = \tilde{F}_k e^{i\pi k/N} = \tilde{F}_k \omega_N^{k/2}
$$
Where $\Large \tilde{F_k}$ indicates the conjugate of $\Large F_k$

---
# Process
* both transforms work on **data sets** that **are neither symmetric nor periodic**
* however, if we extend the data sets according to the symmetry rules, then the reflected (and thus symmetric) sets become periodic as well

The two transformes are connected to the QW-DFT and QW-iDFT via 3-step procedure:
1. extend/duplicate the data set in a symmetric way
2. apply the QW-DFT/QW-iDFT
3. extract the symmetric half of the transformed data set

The equivalance has two important consequences:
1. we may compute the cosine transforms (*N* numbers that require sums over *N* terms => O(N^2) operations) by using an FFT in step 2=> reduce work to O(NlogN)
2. we prove that QW-DCT and QW-iDCT are inverse operations to each other (being a special case of the QW-DFT and QW-iDFT, which are inverse to each other)

---
# Midpoint Rule → Quarter-Wave DFT

$$\Large c_k \simeq \tilde{F}_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n e^{-i2\pi (n+\frac{1}{2})k/N}$$

---
# Symmetry → Cosine Transform

For symmetric data:

$$\Large \tilde{F}_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n \cos\left(\frac{\pi k (n+\frac{1}{2})}{N}\right)$$
see [[Quarter-Wave Discrete Cosine Transform (QW-DCT)]]

---
# Links
[[Algorithms for Scientific Computing]]
[[Quarter-Wave Discrete Cosine Transform (QW-DCT)]]
