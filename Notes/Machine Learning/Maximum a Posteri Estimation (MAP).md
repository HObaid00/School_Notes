Since [[Maximum likelihood Estimation (MLE)]] ignores prior beliefs and performs poorly if little data is available 

MAP estimation says that we should care about the posterior, hence we try to maximize the posterior instead 

> This approach is called maximum a posteriori (MAP) estimation.

$$\Large 
\theta_{MAP} =
\arg\max_\theta p(\theta \ | \ D )  =
\arg\max_\theta \frac{p(D \ | \ \theta) \cdot p(\theta)}{p(D)}
$$
Since $1 / p(D)$  is a positive constant independent of $\theta$ we can ignore it. Leading MAP to be
$$\Large 
\theta_{MAP} = \arg\max_\theta p(D \ | \ \theta) \cdot p(\theta)
$$

---
# Links
[[Machine Learning|Machine Learning]]
[[Bayes sats]]
[[Bayesian Inference]]
[[Maximum likelihood Estimation (MLE)]]
