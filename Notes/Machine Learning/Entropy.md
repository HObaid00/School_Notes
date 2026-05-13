# Impurity Measures (Classification)
With $\Large \pi_c = p(y=c \ | \ t)$:

## Misclassification rate: 
$$\Large i_E(t) = 1 - \max_c \pi_c $$

## Entropy: 
$$\Large i_H(t) = - \sum_{c_i \in C} \pi_{c_i} log_2 \pi_{c_i} $$ (Note that $\Large \lim_\limits{x \to 0^+} \ x \log x = 0$.)

Properties:

- $\Large H = 0$ if node is pure  
- Maximum when distribution is uniform  

## Gini index:
Measure how oftern a randomly chosen instance would be misclassified if it was randomly classified according to the class distribution
$$\Large
i_G(t) = \sum_{c_i \in C} \pi_{c_i} (1 - \pi_{c_i}) = 1 - \sum_{c_i \in C} \pi_{c_i}^2
$$


Properties:

- $\Large G = 0$ if node is pure  
- Maximum when classes are uniformly distributed  
- $\Large \pi_{c_i}$ = probability of picking element
- $\Large 1 -\pi_{c_i}$ = probability of misclassified

![[Pasted image 20260501151427.png]]

#### Entropy vs Gini Index:
* It only matters in 2% of the cases which one you use
* Gini Index small advantage: no need to compute log which can be a bit faster

---
# Shanon Entropy
Expected number of bits needed to encode a randomly drawn value from a distribution (under most efficient code)

For a discrete random variable $X$ with possible values $\{x_1, \dots, x_n \}$
$$\Large
\mathbb{H} = - \sum_{i}^n p(X = x_i)\log_2 p(X = x_i)
$$
![[Pasted image 20260501151803.png]]

Higher entropy -> flatter histogram -> sampled values less predictable
Lower entropy -> peakier histogram -> sampled values more predictable

---
## Information Gain

For split $S$ producing left (L) and right (R) nodes:

$$\Large
IG = I(\text{parent})
- \frac{N_L}{N} I(L)
- \frac{N_R}{N} I(R)
$$

where:

- $I$ is impurity (Gini or entropy)  
- $N$ total samples  
- $N_L$, $N_R$ samples in children  

Choose split maximizing information gain.

---

# Example: Entropy Calculation

Suppose a node contains:

- 4 red  
- 6 blue  

Total: 10 samples

$$\Large
p_{\text{red}} = 0.4, \quad
p_{\text{blue}} = 0.6
$$

Entropy:

$$\Large
H = - (0.4 \log 0.4 + 0.6 \log 0.6)
$$

---
# Links
[[Machine Learning]]