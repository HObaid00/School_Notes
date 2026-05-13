# Logistic Regression

Logistic regression is a probabilistic discriminative classifier.

Despite the name, it is used for classification, not regression.

---

# Model

We directly model:

$$\Large
p(y=1|x)
=
\sigma(w^Tx+w_0)
$$

where:

$$\Large
\sigma(a)=\frac1{1+e^{-a}}
$$

---

# Interpretation

The model outputs class probabilities.

Prediction:

$$\Large
\hat{y}=
\begin{cases}
1 & p(y=1|x)>0.5\\
0 & \text{otherwise}
\end{cases}
$$

---

# Key Difference from LDA

## LDA

Derives probabilities indirectly from generative assumptions.

---

## Logistic Regression

Models probabilities directly.

---

# Advantages

- probabilistic outputs
- differentiable optimization
- often better classification performance

---
# Links
[[Machine Learning]]