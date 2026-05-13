Finding the posterior distribution
$$\Large
p(\theta | \ D)
$$
boils down to finding the normalizing constant, such that the distribution integrates to 1

## Option 1: Brute Force
Compute
$$\Large
 p(D) = \int_0^1 p(D \ |\ \theta)\cdot p(\theta) \ d\theta  
$$
which can be teadious and difficult

## Option 2: Pattern Matching
Look at if the un-normalized posterior looks similar to any known probability density function(PDF) 

---
# Prediction
When we've found $p(D)$ the likelihood of the next stochastic variable is then following Bayes formula

$$\Large
p(\theta | \ D) =  \frac{p(D \ |\ \theta^*)\cdot p(\theta^*)}{p(D)}
$$
---


# Links
[[Machine Learning|Machine Learning]]
[[Bayesian Inference]]
[[Bayes sats]]
