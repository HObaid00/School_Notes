 **Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
Winter Term 2025/2026  

---

# Decision Trees

Decision trees are supervised learning models used for:

- Classification  
- Regression  

They recursively partition the input space into regions with (ideally) homogeneous labels.

![[Pasted image 20260227090318.png|697]]

---

# Basic Idea

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

---

# Tree Construction (Greedy Algorithm)

Top-down recursive partitioning:

1. Start with all data in the root
2. For each feature and candidate split:
   - Compute split quality
3. Choose best split
4. Recurse on child nodes
5. Stop when stopping criterion is met

---

# Impurity Measures (Classification)

Let node contain class proportions:

$$\Large
p_c = \frac{\text{\# samples of class } c}{\text{\# samples in node}}
$$

## 1. Gini Impurity

$$\Large
G = 1 - \sum_{c=1}^C p_c^2
$$

Properties:

- $\Large G = 0$ if node is pure  
- Maximum when classes are uniformly distributed  

---

## 2. Entropy

$$\Large
H = - \sum_{c=1}^C p_c \log p_c
$$

Properties:

- $\Large H = 0$ if node is pure  
- Maximum when distribution is uniform  

---

## Information Gain

For split $S$ producing left (L) and right (R) nodes:

$$\Large
IG = I(\text{parent})
- \frac{N_L}{N} I(L)
- \frac{N_R}{N} I(R)
$$

where:

- $I$ is impurity (Gini or entropy)  
- $N$ total samples  
- $N_L$, $N_R$ samples in children  

Choose split maximizing information gain.

---

# Example: Entropy Calculation

Suppose a node contains:

- 4 red  
- 6 blue  

Total: 10 samples

$$\Large
p_{\text{red}} = 0.4, \quad
p_{\text{blue}} = 0.6
$$

Entropy:

$$\Large
H = - (0.4 \log 0.4 + 0.6 \log 0.6)
$$

---

# Regression Trees

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
# K-fold Cross Validation
* Split your learning data into $\Large K$ folds (10-folds CV is common).
* Use $\Large K-1$ folds for training and the remaining for evaluation
* Average over all folds to get an estimate
	* of the error for a setting of your *hyper-parameter*
	* or the model for your model selection
* Try different settings for your hyper-parameters.
* Use all your training data and the best hyper-parameters for final training ( and testing) of your model

![[Pasted image 20260227092634.png]]

---
# LOOCV - The extreme Case

In leave-one-out-cross validation (LOOCV) we train on all but one
sample.

If we have N samples, this is the same as N -fold cross-validation.

LOOCV is interesting if we do not have a lot of data and we want to use as much of it for training as possible but still get a good estimate of model performance.

But it also means that we need to train our model N times...

If we have sufficiently large amounts of data and training our model is computationally expensive, we better stick to lower numbers of K or a single validation set.

---
# Pruning

Two strategies:

## 1. Pre-pruning

Stop early using stopping criteria.

## 2. Post-pruning

1. Grow full tree  
2. Remove branches that do not improve validation performance  

---

# Cost-Complexity Pruning

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

# Properties of Decision Trees

Advantages:

- Easy to interpret  
- Handle categorical and numerical data  
- No feature scaling required  
- Nonlinear decision boundaries  

Disadvantages:

- High variance  
- Prone to overfitting  
- Unstable (small data changes → different tree)  

---

# Axis-Aligned Splits

Standard trees create splits of form:

$$\Large
x_j \le t
$$

This creates axis-aligned partitions.

*(Copy figure showing rectangular regions on slide.)*

---

# Limitations

- Cannot easily model oblique boundaries  
- Greedy training may not find optimal tree  
- Performance often worse than ensemble methods  

---

# Computational Complexity

Training:

- For each node: evaluate many candidate splits  
- Roughly $\Large O(N D \log N)$ for balanced trees  

Prediction:

- $\Large O(\text{depth})$

---

# Summary

We covered:

- Decision tree construction  
- Gini impurity and entropy  
- Information gain  
- Regression trees  
- Overfitting and pruning  
- Strengths and weaknesses  

---

# Reading

Main:

- Murphy, *Machine Learning: A Probabilistic Perspective*  

Extra:

- Hastie, Tibshirani, Friedman  
  *The Elements of Statistical Learning*  

---

# Next Lecture

Ensemble methods:

- Random Forests  
- Boosting  