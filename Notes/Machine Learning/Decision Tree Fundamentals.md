# Fundamentals
Given training data:

$$\Large
D = \{(x_i, y_i)\}_{i=1}^N
$$

Goal: Learn a tree that splits the feature space such that:
- Leaves contain samples that are “pure”
- Predictions are constant within each leaf

Each internal node tests a feature:

- For numerical features: threshold split  
$$\Large
x_j \le t
$$
- For categorical features: subset test  

![[Pasted image 20260227091043.png]]

![[Pasted image 20260501140300.png|692]]


---
# Binary Split
Simplest decision: binary split on a single feature $\Large x_i \le a$ 
Distribution of classes in leaf: (red, green, blue)

![[Pasted image 20260501140506.png]]

---
# Interpretation of a decision tree
The graph consists of nodes, branches and leafs:
* Node = feature test => leads to decision boundary
* Branch = different outcome of the preceding feature test
* Leaf = region in the input space and the distribution of samples in that region

---
# Inference on decision trees
To classify a new sample x:
* test the attributes of x to find the region R that contains it and get the class distribution  $\Large n_R = (n_{c_1 , R} n_{c_2 , R}, \dots, n_{c_n , R})$ for $\Large C = \{c_1, \dots, c_k\}$.
* The probability that a data point $\Large x \in R$ should be classified belonging to class c is then $$\Large p(y=c \ | \ R) = \frac{n_{c, R}}{\sum_{c_i \in C} n_{c_i, R} } $$
* A new unseen sample x is simply given the label which is most common in its corresponding region: $$\Large \hat{y} = \arg\max_c \ p(y=c \ | \ x) = \arg\max_c \ p(y=c \ | \ R) = \arg\max_c  n_{c, R}$$
---
# Optimal decision tree
#### Generalization: 
Find a DT that performs well on new (unseen) data.

Again split the dataset
![[Pasted image 20260501142325.png]]

* build tree from training set $\Large D_T$,
* predict *validation* set labels  $\Large \hat{y}_i$ using the tree,
* evaluate by comparing predictions $\Large \hat{y}_i$ to true labels $\Large {y}_i$. 
* pick the tree that performs the best on the validation set
* report final performance on the test set

#### Building the optimal decision tree is intractable
Iterating over all possible trees is possible only for very small examples because the number of trees quickly explodes.

Finding the optimal tree is *NP-complete*.

**Instead:** grow the tree top-down and choose the best split node-by-node using **greedy heuristic** on the *training data*

![[Pasted image 20260501145250.png]]

---

# Links
[[Machine Learning]]