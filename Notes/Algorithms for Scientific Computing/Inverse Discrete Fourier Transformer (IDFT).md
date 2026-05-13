# Definition
The Inverse Discrete Fourier Transform (IDFT) of the vector $(F_0, \dots , F_{N-1})$ is given by the vector $(f_0, \dots, f_{N-1})$ where
$$\Large
f_n = \sum_{k=0}^{N-1} F_k e^{i2\pi nk/N}
$$

# Observation
DFT and IDFT are inverse operations
$$\Large
F_k = \frac{1}{N} \sum_{n=0}^{N-1} f_n e^{-i2\pi nk/N} 
$$
$$\Large
F = DFT(IDFT(F))
$$
or 

$$\Large
f_n = \sum_{k=0}^{N-1} F_k e^{i2\pi nk/N}
$$ $$\Large
f = IDFT(DFT(f))$$
---
# Links
[[Algorithms for Scientific Computing]]
