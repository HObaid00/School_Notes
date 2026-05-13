To represent prior beliefs about a given distribution $\Large \theta$ we introduce$$\Large p(\theta) $$

---
# Choose $\theta$ 

1. It must not depend on the data
2. $$\Large p(\theta) \geq 0 \quad \forall \ \theta$$ 
3. $$\Large \int p(\theta) \ d\theta = 1$$
---
# Bayes Formula
[[Bayes sats]] tells us how to update our beliefs about $\Large \theta$ after observing the data $\Large D$: 
$$\Large
p(\theta \ | \ D) = \frac{p(D \ | \ \theta) \cdot p(\theta)}{p(D)}
$$
Here, $\Large p(\theta \ | \ D)$ is the posterior distribution. 

---
# Posterior
The posterior depends on the following terms:
* $\Large p(\theta \ | \ D)$ is the likelihood
* $\Large p(\theta)$ is the prior that encodes our beliefs before observing data
* $\Large p(D)$ is the evidence. It acts as a normalizing constant that ensures that the posterior distribution integrates to 1.
$$\Large
\text{posterior} \propto \text{likelihood} \ \cdot \ \text{prior}
$$
Meaning the posterior is proportional to the likelihood distribution times the prior distribution.

Usually, we define our model by specifying the likelihood and the prior. We obtain the evidence using the sum rule of probability
$$\Large
p(D) = \int p(D, \theta)\ d\theta = \int p(D \ | \ \theta)\cdot p(\theta) \ d\theta
$$
The Bayes formula tells us how to update our beliefs give the data

![[Pasted image 20260502125708.png]]

Observing more data increases our confidence

![[Pasted image 20260502125746.png]]

---
# Links
[[Machine Learning]]
[[Bayes sats]]

