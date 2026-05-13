### White Noise Spectrum
To measure White Noise Quality  
#### Spectral Flatness Measure (SFM)  
  
A simple KPI for evaluating white noise is the Spectral Flatness Measure.  
  
$$\Large  
SFM=  
\frac{  
\left(  
\prod_{i=1}^{N} P_i  
\right)^{1/N}  
}{  
\frac{1}{N}\sum_{i=1}^{N}P_i  
}  
$$  
  
Where:  
- $P_i$ = power at frequency bin $i$  
- $N$ = number of frequency bins  
  
---  
  
#### Interpretation  
  
| SFM Value   | Meaning                          |     |
| ----------- | -------------------------------- | --- |
| $\approx 1$ | Good white noise (flat spectrum) |     |
| $\approx 0$ | Uneven or tonal signal           |     |
  
Higher SFM values indicate:  
- more uniform frequency distribution,  
- better white noise quality,  
- stronger spectral flatness.

---
### Links
[[Edge Computing & IoT]]