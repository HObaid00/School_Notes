**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
Winter Term 2025/2026  

---

# Coin Flip Example

We flip the same coin 10 times:

H T H H T H H H T H  

Question: What is the probability that the next flip is T?

---

# Modeling Coin Flips

For the i-th coin flip:

$$\Large
p(F_i = T) = \theta_i
$$

More precisely:

$$\Large
p(F_i = T \mid \theta_i) = \text{Ber}(F_i = T \mid \theta_i) = \theta_i
$$

i.e.

$$
F_i \sim \text{Ber}(\theta_i)
$$

We want to reason about $\Large \theta_{11}$.

---

# Section 1: Maximum Likelihood Estimation (MLE)

Assumptions:

1. Identical distribution:

$$\Large
p(F_i = f_i \mid \theta_i) = p(F_i = f_i \mid \theta)
$$

2. Independence:

$$\Large
p(F_1, \dots, F_{10} \mid \theta)
=
\prod_{i=1}^{10} p(F_i = f_i \mid \theta)
$$

Thus, flips are i.i.d.

---

# Likelihood Function

Observed data:

H T H H T H H H T H  

Number of T: $|T| = 3$  
Number of H: $|H| = 7$

Likelihood:

$$\Large
p(D \mid \theta)
=
\theta^3 (1 - \theta)^7
$$

Define:

$$\Large
f(\theta) := p(D \mid \theta)
$$

MLE:

$$\Large
\theta_{\text{MLE}}
=
\arg\max_{\theta \in [0,1]} f(\theta)
$$

Important: The likelihood is **not** a probability distribution over $\theta$.

---

# Log-Likelihood Trick

Monotonicity:

$$\Large
\arg\max_\theta f(\theta)
=
\arg\max_\theta \log f(\theta)
$$

MLE solution:

$$\Large
\theta_{\text{MLE}}
=
\frac{|T|}{|T| + |H|}
$$

Prediction:

$$\Large
F_{11} \sim \text{Ber}(\theta_{\text{MLE}})
$$

---

# Problem with MLE

Example: H H

$$\Large
\theta_{\text{MLE}} = 0
$$

But a fair coin ($\theta = 0.5$) still has 25% chance to produce HH.

MLE ignores prior beliefs.

---

# Section 2: Bayesian Inference

Introduce prior:

$$\Large
p(\theta)
$$

Constraints:

- $\Large p(\theta) \ge 0$
- $\Large\int p(\theta)\, d\theta = 1$
- $\Large\theta \in [0,1]$

---

# Bayes' Rule

$$\Large
p(\theta \mid D)
=
\frac{p(D \mid \theta)p(\theta)}{p(D)}
$$

where:

- Likelihood: $p(D \mid \theta)$
- Prior: $p(\theta)$
- Evidence:

$$\Large
p(D)
=
\int p(D \mid \theta)p(\theta)\, d\theta
$$

Posterior ∝ Likelihood × Prior

---

# Section 3: Maximum A Posteriori (MAP)

Instead of MLE:

$$\Large
\theta_{\text{MAP}}
=
\arg\max_\theta p(\theta \mid D)
$$

Equivalent to:

$$\Large
\arg\max_\theta p(D \mid \theta)p(\theta)
$$

---

# Beta Prior

Choose:

$$\Large
\text{Beta}(\theta \mid a,b)
=
\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}
\theta^{a-1}(1-\theta)^{b-1}
$$

with $\Large a>0$, $\Large b>0$.

---

# Posterior Distribution

Likelihood:

$$\Large
p(D \mid \theta)
=
\theta^{|T|}(1-\theta)^{|H|}
$$

Prior:

$$\Large
p(\theta)
=
\theta^{a-1}(1-\theta)^{b-1}
$$

Posterior:

$$\Large
p(\theta \mid D)
\propto
\theta^{|T|+a-1}(1-\theta)^{|H|+b-1}
$$

Thus:

$$\Large
p(\theta \mid D)
=
\text{Beta}(\theta \mid a+|T|, b+|H|)
$$

Beta is conjugate prior for Bernoulli.

---

# MAP Solution

$$\Large
\theta_{\text{MAP}}
=
\frac{|T| + a - 1}
{|T| + |H| + a + b - 2}
$$

If $\Large a=b=1$ (uniform prior):

$$
\theta_{\text{MAP}} = \theta_{\text{MLE}}
$$

---

# Section 4: Full Posterior

Posterior:

$$\Large
p(\theta \mid D)
=
\text{Beta}(a+|T|, b+|H|)
$$

We now have:

- Mean
- Variance
- Credible intervals

More data → posterior becomes more concentrated.

---

# Frequentist View

Hoeffding's inequality:

$$\Large
p(|\theta_{\text{MLE}} - \theta| \ge \varepsilon)
\le
2e^{-2N\varepsilon^2}
$$

To achieve error $\varepsilon$ with probability $1-\delta$:

$$\Large
N
\ge
\frac{\ln(2/\delta)}{2\varepsilon^2}
$$

---

# Section 5: Posterior Predictive Distribution

Goal:

$$\Large
p(F = f \mid D, a, b)
$$

Using:

$$\Large
p(f \mid D)
=
\int_0^1 p(f \mid \theta)p(\theta \mid D)\, d\theta
$$

Since:

$$\Large
p(f \mid \theta)
=
\theta^f (1-\theta)^{1-f}
$$

We obtain:

$$\Large
p(f \mid D)
=
\text{Ber}
\left(
f \mid
\frac{|T| + a}{|T| + |H| + a + b}
\right)
$$

This is fully Bayesian prediction.

---

# Comparison of Predictions

- MLE:

$$\Large
\frac{|T|}{|T|+|H|}
$$

- MAP:

$$\Large
\frac{|T|+a-1}{|T|+|H|+a+b-2}
$$

- Fully Bayesian:

$$\Large
\frac{|T|+a}{|T|+|H|+a+b}
$$

As data increases → all methods converge.

---

# Key Concepts

- Maximum Likelihood Estimation  
- Maximum A Posteriori  
- Fully Bayesian Analysis  
- Prior, Likelihood, Posterior  
- i.i.d. assumption  
- Conjugate priors  
- Marginalization  
- Posterior predictive distribution  

---

# Reading

Murphy, *Machine Learning: A Probabilistic Perspective*  
Chapters 3.1–3.3  

Slides based on earlier version by M. Sölch.