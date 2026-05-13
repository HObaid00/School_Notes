# Probabilistic Classification

Instead of predicting only labels, probabilistic models estimate:

$$\Large
p(y=c|x)
$$

the probability that input $x$ belongs to class $c$.

---

# Bayes' Rule

The posterior probability is:

$$\Large
p(y=c|x)
=
\frac{
p(x|y=c)p(y=c)
}{
p(x)
}
$$
or more compactly 

$$
\Large
p(y=c|x)
\propto
p(x|y=c) p(y=c)
$$

Meaning the prediction is proportional to the distribution

---

# Components

## Class Prior

$$\Large
p(y=c)
$$

Probability of class $c$ before seeing data.

---

## Class Conditional

$$\Large
p(x|y=c)
$$

Probability of generating $x$ from class $c$.

---

## Posterior

$$
\Large
p(y=c|x)
$$

Probability of class given observed data.

---

## Learning Procedure

1. Choose parametric forms:
   - $p(x|y=c,\psi)$
   - $p(y=c|\theta)$
2. Estimate parameters via ML
3. Perform inference:

$$\Large
p(y=c|x)
\propto
p(x|y=c,\hat{\psi}) p(y=c|\hat{\theta})
$$

Also allows data generation.

---

# Prediction Rule

Usually:

$$\Large
\hat{y}
=
\arg\max_c p(y=c|x)
$$

---

# Two Types of Models

## Generative

Model:

$$\Large
p(x,y)
$$

---

## Discriminative

Model:

$$\Large
p(y|x)
$$

directly.

---
# Links
[[Bayes sats]]
[[Bayesian Inference]]
[[Machine Learning]]