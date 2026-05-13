
# Definition
Given a training dataset

$$\Large
D = \{(x_i, y_i)\}_{i=1}^N
$$

where:

- $\Large x_i \in \mathbb{R}^D$ are features  
- $\Large y_i \in \{1, \dots, C\}$ are class labels  

---
# To classify new observations:

1. Define a distance measure (e.g., Euclidean distance)
2. Compute the nearest neighbor for each new data point
3. Assign the label of the nearest neighbor

Works for both classification and regression.

---

## 1-NN and Voronoi Tessellation

1-NN induces a Voronoi tessellation of the space.

This often results in **poor generalization**.

![[Pasted image 20260226171608.png|697]]

---
# Links
[[Machine Learning]]
