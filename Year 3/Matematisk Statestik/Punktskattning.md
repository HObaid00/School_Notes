# Matematisk statistik
Eric Järpe

## F 10: Punktskattning

Eric Järpe  
ITE  
Högskolan i Halmstad  
10 november 2025

---

# Punktskattning

## Exempel

Inför ett val:

- opinionsundersökning / prognoser (stickprov)
- valet (totalundersökning) med partiella prognoser under rösträkningen

---

## Logiken

Av de $n$ observationerna i stickprovet räknas andelen som röstar på ett visst parti.

Detta ger en **skattning**.

---

De $N-n$ återstående individerna kan rösta annorlunda → prognosen kan bli fel.

Dock är detta **osannolikt** om stickprovet är representativt.

---

Det finns alltid **slumpmässiga avvikelser** som beror på

- stickprovsstorlek
- skillnader i andelar
- feedbackeffekter

---

Därför behövs en modell med **stokastiska variabler** som gör det möjligt att ange **säkerhet i skattningen**.

---

# Definition

En punktskattning av en parameter $\theta$ är en funktion av variablerna i ett stickprov:

$$
\theta^*_{obs} = \theta^*(x_1,x_2,\dots,x_n)
$$

(observerat värde)

---

Den stokastiska motsvarigheten är

$$
\theta^* = \theta^*(X_1,X_2,\dots,X_n)
$$

---

## Väntevärdesriktig skattning

En punktskattning $\theta^*_{obs}$ är **väntevärdesriktig (vvr)** om

$$
E(\theta^*) = \theta
$$

---

## Konsistens

Skattningen är **konsistent** om

$$
\lim_{n\to\infty} P(|\theta^*_n-\theta|>\varepsilon)=0
$$

för varje

$$
\varepsilon>0
$$

---

## Medelkvadratfel

$$
MSE = E((\theta^*_n - \theta)^2)
$$

---

## Effektivitet

Antag två väntevärdesriktiga skattningar

$$
\theta^*_{obs}
$$

och

$$
\hat{\theta}_{obs}
$$

för parametern $\theta$.

---

Om

$$
V(\theta^*) \le V(\hat{\theta})
$$

för alla $\theta$ och

$$
V(\theta^*) < V(\hat{\theta})
$$

för något $\theta$

så är

$$
\theta^*_{obs}
$$

**effektivare**.

---

# Exempel

Antag att livslängden för komponenter är

$$
X \in Exp(\lambda)
$$

---

Vi vill skatta $\lambda$ med

$$
\lambda_1^* = C_1\bar{x}
$$

eller

$$
\lambda_2^* = C_2 \min_{1\le i\le n} X_i
$$

---

## a) Bestäm $C_1$ och $C_2$ så att skattningarna är vvr

---

### För $\lambda_1^*$

$$
E(\bar{X}) = \frac{1}{n}\sum_{i=1}^n E(X_i)
$$

---

Eftersom

$$
E(X_i)=\frac{1}{\lambda}
$$

får vi

$$
E(\bar{X})=\frac{1}{\lambda}
$$

---

Alltså

$$
E(\lambda_1^*) = C_1E(\bar{X})
$$

---

För väntevärdesriktighet krävs

$$
C_1 = \lambda^2
$$

---

Alltså

$$
\lambda_1^* = \lambda^2\bar{X}
$$

---

### För $\lambda_2^*$

Låt

$$
Z=\min_{1\le i\le n} X_i
$$

---

Fördelningsfunktion

$$
F_Z(z)=P(Z\le z)
$$

---

$$
=1-P(Z>z)
$$

---

$$
=1-P(X_1>z)P(X_2>z)\dots P(X_n>z)
$$

---

Eftersom

$$
P(X_i>z)=e^{-\lambda z}
$$

---

$$
F_Z(z)=1-e^{-n\lambda z}
$$

---

Alltså

$$
Z\in Exp(n\lambda)
$$

---

och

$$
E(Z)=\frac{1}{n\lambda}
$$

---

Därför

$$
E(\lambda_2^*) = C_2E(Z)
$$

---

För väntevärdesriktighet krävs

$$
C_2=n\lambda^2
$$

---

Alltså

$$
\lambda_2^* = n\lambda^2 \min_{1\le i\le n}X_i
$$

---

# b) Vilken skattning är effektivast?

---

### Varians för $\lambda_1^*$

$$
V(\lambda_1^*)
=
V(\lambda^2\bar{X})
$$

---

$$
=
\lambda^4 V(\bar{X})
$$

---

Eftersom

$$
V(\bar{X})=\frac{1}{n^2}\sum_{i=1}^n V(X_i)
$$

---

och

$$
V(X_i)=\frac{1}{\lambda^2}
$$

---

får vi

$$
V(\lambda_1^*)
=
\frac{1}{n}\lambda^2
$$

---

### Varians för $\lambda_2^*$

$$
V(\lambda_2^*)
=
V(n\lambda^2 \min X_i)
$$

---

$$
=
n^2\lambda^4 V(\min X_i)
$$

---

Eftersom

$$
\min X_i \in Exp(n\lambda)
$$

---

$$
V(\min X_i)=\frac{1}{(n\lambda)^2}
$$

---

Alltså

$$
V(\lambda_2^*)=\lambda^2
$$

---

### Jämförelse

$$
V(\lambda_1^*)=\frac{1}{n}\lambda^2
$$

---

$$
V(\lambda_2^*)=\lambda^2
$$

---

För alla

$$
n=1,2,3,\dots
$$

gäller

$$
V(\lambda_1^*) \le V(\lambda_2^*)
$$

---

Alltså är

$$
\lambda_1^*
$$

**effektivare**.

---

# Skattningar av medelvärde och varians

Eftersom

$$
\mu^*_{obs}=\bar{x}
$$

är

$$
\mu^*=\bar{X}
$$

---

## Sats

$\bar{x}$ är

- väntevärdesriktig
- konsistent

skattning av

$$
\mu
$$

(Bevisas med **Chebyshevs olikhet**.)

---

# Variansskattning

Observerad skattning

$$
(\sigma^2)^*_{obs} = s^2
$$

---

där

$$
s^2=
\frac{1}{n-1}
\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

---

Stokastisk motsvarighet

$$
S^2=
\frac{1}{n-1}
\sum_{i=1}^{n}(X_i-\bar{X})^2
$$

---

## Sats

$s^2$ är

- väntevärdesriktig
- konsistent

skattning av

$$
\sigma^2
$$e