---
aliases:
  - Normal Distribution
  - Gaussian Distribution
---
## Definition
Normaliserad distrubition med $0$ är i mitten efter normalization. Beskriver "naturliga fenomen". 

Att X är normalfördelad betecknas 

$$\Large
\begin{array}s
X \in N(\mu,\sigma ^2) \\
\mu \in \mathbb{R} \\
\sigma ^2 \in \mathbb{R}^+
\end{array}
$$
## Värderum
$$\Large
S=\mathbb{R}
$$
## Täthetsfunktion

$$\Large
\varphi(x)=f(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

## Fördelningsfunktion

$$\Large
 \Phi(x)=F(x)=
\frac{1}{\sqrt{2\pi}\sigma}
\int_{-\infty}^{x} e^{-\frac{(t-\mu)^2}{2\sigma^2}} dt
$$
![[Pasted image 20260419141742.png]]

## Symmetri
$$\Large
\varphi(-x) = \varphi(x) \ \text{jämn funktion} \ \Rightarrow \Phi(-x) = 1 - \Phi(x) 
$$

## Intervall
$$\Large
P(a \le X \le b) = \Phi(b) - \Phi(a)
$$
## Percentil:
$$\Large
\lambda_\alpha : P(X \ge \lambda_\alpha) = \alpha
$$
## Allmän normalfördelning Satser och Observationer
### Sats 1
$$\Large
X \in N(\mu, \sigma) \iff \frac{X-\mu}{\sigma} \in N(\mu, \sigma)
$$
Om det som står ovan stämmer innebär:
$$\Large
F(X)=\Phi(\frac{x-\mu}{\sigma}) \ \text{och} \ f(x) = \frac{1}{\sigma}\phi(\frac{x-\mu}{\sigma})
$$
### Observation 1
Om
$$\Large
P(a \le X \le b) = \Phi(\frac{b-\mu}{\sigma}) - \Phi(\frac{a-\mu}{\sigma})
$$

### Sats 2 - Oberoende Sats
Om 
$$\Large
X \in N(\mu_X, \sigma_X) \ \text{oberoende av} \ Y \in N(\mu_Y, \sigma_Y)
$$
så
$$\Large
X + Y \in N(\mu_X + \mu_Y, \sqrt{\sigma_X ^2 + \sigma_Y ^2 })
$$
och 
$$\Large
X - Y \in N(\mu_X - \mu_Y, \sqrt{\sigma_X ^2 + \sigma_Y ^2 })
$$
### Observation 2 Stickprov
Om 
$$\Large
X_1, X_2, \dots, X_n \quad X_i 
\in N(\mu_X, \sigma_X) \Rightarrow 
\bar{X} \in N(\mu_X, \frac{\sigma_X}{\sqrt{n}})
$$
och 
$$\Large
Y_1, Y_2, \dots, Y_n \quad Y_i 
\in N(\mu_Y, \sigma_Y) \Rightarrow 
\bar{Y} \in N(\mu_Y, \frac{\sigma_Y}{\sqrt{n}})
$$
då blir 
$$
\Large
\bar{X} - \bar{Y} \in N(\mu_X - \mu_Y, \sqrt{\frac{\sigma_X ^2}{n} + \frac{\sigma_Y ^2}{n}})
$$
---
