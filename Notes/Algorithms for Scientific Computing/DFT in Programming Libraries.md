Different conventions for sign factors in exponent, normalization factors etc.
* Python/Numpy: numpy.fft; normalization factor $1/N$ in *inverse* transform by default
* Matlab, IMSL, (Int. Math. and Stat. Library):
$$\Large
F_{k+1} = \sum_{n=0}^{N-1} f_{n+1} e^{-i2\pi nk/N}, \quad k= 0, \ \dots, \ N-1
$$
$$\Large
f_{n+1} = \frac{1}{N}\sum_{k=0}^{N-1} F_{k+1} e^{i2\pi nk/N} \quad n = 0, \ \dots, \ N-1
$$
* Maple $1/\sqrt{N}$ as factor for DFT and IDFT

### Index shift by +1, since:
* Data/coefficients start at index 0
* Arrays to store the numbers start at index 1
