# DFT och FFT

DFT används för frekvensanalys av ändliga sekvenser och implementeras effektivt med FFT.

## Definition
$$\Large
X[k] = \sum_{n=0}^{N-1} x[n] e^{-\frac{jk 2πn}{N}}
$$
## Viktigt
- frekvensaxeln delas i N steg
- både $x[n]$ och $X[k]$ blir periodiska med period $N$
- FFT är en snabb algoritm för att beräkna DFT

## Komentar
DFT beskrivs som det centrala verktyget för frekvensanalys av mätdata.

## Länkar
- [[DTFS]]
- [[DTFT]]
- [[Samplingsteoremet]]