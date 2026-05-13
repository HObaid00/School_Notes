
Instead of classification impurity, minimize squared error.

Prediction in leaf:

$$\Large
\hat{y} =
\frac{1}{N} \sum_{i \in \text{leaf}} y_i
$$

Split quality:

Minimize

$$\Large
\sum_{i \in L} (y_i - \bar{y}_L)^2
+
\sum_{i \in R} (y_i - \bar{y}_R)^2
$$

---

# Stopping Criteria

Common criteria:

- Maximum depth reached  
- Minimum number of samples per node  
- No improvement in impurity  
- Node is pure  

---

# Overfitting

Deep trees:

- Very low training error  
- Poor generalization  

![[Pasted image 20260227092209.png|697]]

![[Pasted image 20260227092239.png|697]]

---
# Links
[[Machine Learning]]