# Pruning

Two strategies:

## 1. Pre-pruning

Stop early using stopping criteria.

## 2. Post-pruning

1. Grow full tree  
2. Remove branches that do not improve validation performance  

---

# Cost-Complexity of Pruning

Objective:

$$\Large
R_\alpha(T) =
R(T) + \alpha |T|
$$

where:

- $\Large R(T)$ = empirical error  
- $\Large |T|$ = number of leaves  
- $\alpha$ = regularization parameter  

Choose $\alpha$ via validation.

---
# Links
[[Machine Learning]]
