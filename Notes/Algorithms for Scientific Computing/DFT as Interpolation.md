# DFT as the Solution of an Interpolation Problem

**Interpolation Problem**:
* *N* ansatz function: $$\Large g_k(x):=e^{ikx} \in [0, 2\pi ], \ k = 0, \dots , N-1$$
* *N* supporting points: $$\Large x_n:=  2\pi n / N, \ n = 0, \dots, N-1$$
* *N* interpolation value $$\Large f_n, \ n = 0, \dots, N-1 $$
* find *N* weights $F_k$ such that at all supporting points $$\Large f_n = \sum_{k=0}^{N-1} F_k g_k (x_n) \quad \iff \quad f_n = \sum_{k=0}^{N-1} F_k e^{i2 \pi n k/N}$$ **"trigonometric interpolation"** 

---
# Formulation via Complex Polynomials
**Interpolation problem**
* *N* ansatz funtion (complex unit polynomials), k = 0, ..., N-1: $$\Large \tilde{g_k}(z) := z^k $$
* *N* supporting points: $$\Large z_n := e^{i2 \pi n/N}= \omega_N^n \; \text{where} \; \omega_N := e^{i2\pi /N}$$
* *N* interpolation values $$\Large  f_n , \; n = 0, \dots , N-1$$ respectively.
* find the *N* weights $F_k$ such that at all supporting points $$\Large f_n \sum_{k=0}^{N-1} F_k \tilde{g_k} (z_n) \quad \iff \quad f_n = \sum_{k=0}^{N-1} F_k e^{i2 \pi n k/N}$$ Polynomial interpolation at the ***"complex unit roots"*** $\Large \omega_N^n$ 

---
## Interpretation of the Interpolation Problem
Starting from the first formulation,
$$\Large
f_n = \sum_{k=1}^{N-1} F_k g_k(x_n), \quad g_k(x_n) = e^{i2\pi n k /N},
$$
we look for a representation of the signal $f_n$  - or of a function $f(x)$ - of the form 
$$\Large
f_n = \sum_{k=1}^{N-1} F_k g_k(x), \quad g_k(x) = e^{i2\pi k  x}
$$
The ansatz functions are sine or cosine oscillations:
$$\Large
e^{ikx} = cos (kx) + i sin(kx)
$$
---
## Conclusions:
* we look for the **representation of a periodic function** as a sum of sine and cosine modes
* the $F_k$ are, thus, called **Fourier coefficients:
	* k represents the wave number
	* the value of $F_k$ represents the amplitude of the corresponding frequency
* the Fourier transform leads to a **frequency spectrum**
* useful when a problem is easier to solve in the **frequency domain** than in the **spatial domain**.

![[Pasted image 20260420145612.png]]

---

# Solution of the Interpolation Problem 
Both interpolation problems lead to the identical linear systems of equations
$$\Large
f_n = \sum_ {k=0}^{N-1} F_k \omega_N^{nk}, \; \text{for all } n = 0, \dots, N-1;
$$
where 
$$\Large
\omega_N := e^{i2 \pi / N} \; \text{i.e.} \; \omega_N ^{nk} := e^{i2 \pi nk / N}
\quad \text{"unit roots": }  \omega_N^N = 1
$$
If we write the vectors of the $f_n$ and $F_k$ as $f  := (f_0, \dots , f_{N-1})$  and $F := (F_0, \dots , F_{N-1})$ , the linear system of equations can be formulated in matrix notation 
$$\Large
WF = \bar{f}$$
where the entries of the **Fourier matrix W** are given by 
$$\Large
W_{nk} := \omega_N^{nk}
$$
**Next Step(s):** Show that system can be solved with effort $\mathcal{O}(N^2)$ - and using FFT even only $\mathcal{O}(NlogN)$ - instead of $\mathcal{O}(N^3)$   

---
