# Mathematical Equations for Sound Masking System KPIs

## 1. Signal-to-Noise Ratio (SNR)

Measures how dominant speech is relative to masking noise.

$$\Large
\text{SNR}_{dB}=10\log_{10}\left(\frac{P_{speech}}{P_{noise}}\right)
$$

or using amplitudes:

$$\Large
\text{SNR}_{dB}=20\log_{10}\left(\frac{A_{speech}}{A_{noise}}\right)
$$

Where:
- $P_{speech}$ = speech power
- $P_{noise}$ = masking noise power
- $A_{speech}$ = speech amplitude
- $A_{noise}$ = masking noise amplitude

Lower SNR implies better masking performance.

---

## 2. Speech Privacy Index (SPI)

Simplified approximation:

$$\Large
\text{SPI}=1-\text{Speech Intelligibility}
$$

Using Speech Intelligibility Index (SII):

$$\Large
\text{SPI}=1-\sum_{i=1}^{n} B_iA_i
$$

Where:
- $B_i$ = importance of frequency band
- $A_i$ = audibility in frequency band

Higher SPI indicates greater speech privacy.

---

## 3. Root Mean Square (RMS) Amplitude

Measures microphone signal intensity.

$$\Large
A_{RMS}=\sqrt{\frac{1}{N}\sum_{i=1}^{N}x_i^2}
$$

Where:
- $x_i$ = audio sample
- $N$ = number of samples

Used for adaptive gain and amplitude tracking.

---

## 4. Sound Pressure Level (SPL)

Measures sound loudness in decibels.

$$\Large
L_p=20\log_{10}\left(\frac{p}{p_0}\right)
$$

Where:
- $p$ = measured sound pressure
- $p_0=20\mu Pa$ = reference pressure

---

## 5. Power Spectral Density (PSD)

Measures frequency-domain energy distribution.

$$\Large
PSD(f)=\frac{|X(f)|^2}{N}
$$

Where:
- $X(f)$ = Fourier transform of signal
- $N$ = signal length

Used to validate generated noise spectra.

---

## 6. Pink Noise Spectrum

Ideal pink noise distribution:

$$\Large
P(f)\propto\frac{1}{f}
$$

Equal energy exists per octave.

---

## 7. Brown Noise Spectrum

Ideal brown noise distribution:

$$\Large
P(f)\propto\frac{1}{f^2}
$$

Emphasizes lower frequencies more strongly.

---

## 8. System Latency

Measures total input-to-output delay.

$$\Large
\text{Latency}=t_{output}-t_{input}
$$

Where:
- $t_{input}$ = microphone capture time
- $t_{output}$ = speaker playback time

Target latency is typically below $20\,ms$.

---

## 9. Adaptive Response Time

Measures how quickly the system reacts to sound changes.

$$\Large
T_{response}=t_{stable}-t_{change}
$$

Where:
- $t_{change}$ = time environmental change occurs
- $t_{stable}$ = time masking stabilizes

---

## 10. Mean Squared Error (MSE)

Compares generated spectrum to ideal spectrum.

$$\Large
MSE=\frac{1}{N}\sum_{i=1}^{N}(y_i-\hat{y}_i)^2
$$

Where:
- $y_i$ = ideal spectrum
- $\hat{y}_i$ = generated spectrum

Lower MSE indicates more accurate noise generation.

---

## 11. Total Harmonic Distortion (THD)

Measures unwanted harmonic distortion.

$$\Large
THD=\frac{\sqrt{V_2^2+V_3^2+\cdots+V_n^2}}{V_1}
$$

Where:
- $V_1$ = fundamental frequency amplitude
- $V_n$ = harmonic amplitudes

Lower THD corresponds to cleaner audio output.

---

## 12. Packet Loss Rate

Applicable for distributed IoT systems.

$$\Large
\text{Packet Loss Rate}=
\frac{Packets_{lost}}{Packets_{sent}}\times100
$$

---

## 13. CPU Utilization

Measures edge device processing load.

$$\Large
CPU\ Usage=
\frac{T_{active}}{T_{total}}\times100
$$

Where:
- $T_{active}$ = processor active time
- $T_{total}$ = total observation time

---

## 14. Energy Consumption

Measures system energy usage.

$$\Large
E=P\times t
$$

Where:
- $P$ = power consumption
- $t$ = operating time

---

## 15. Masking Efficiency

Measures effectiveness of intelligibility reduction.

$$\Large
\text{Masking Efficiency}=
\frac{I_{before}-I_{after}}{I_{before}}
$$

Where:
- $I_{before}$ = speech intelligibility before masking
- $I_{after}$ = speech intelligibility after masking

Higher values indicate more effective sound masking.