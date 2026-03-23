**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
Winter Term 2025/2026  

---

# Unsupervised Learning

## Main Idea

Given unlabeled data:

$$\Large
\{x_i\}_{i=1}^N
$$

discover latent structure.

Last week:
- Dimensionality reduction  
  $$\Large
  x_i \in \mathbb{R}^D
  \;\to\;
  z_i \in \mathbb{R}^K, \quad K \ll D
  $$

This week:
- Clustering  
  Group objects $x_i$ into $K$ clusters based on similarity.

---

# Clustering: Examples

- Image segmentation  
- User profiling  
- Gene expression analysis  
- Data compression  
- Visualization  

![[Pasted image 20260228190538.png]]

---

# Problem Definition

Given:

$$\Large
X = \{x_1, \dots, x_N\}
$$

Find assignments:

$$\Large
z_i \in \{1, \dots, K\}
$$

such that:

- Within-cluster similarity is high  
- Between-cluster similarity is low  

---

# Section 1 — K-means Algorithm

## Distance-Based Clustering

Define similarity or distance:

- Manhattan distance:
  $$\Large
  d(x_i, x_j)
  =
  \|x_i - x_j\|_1
  $$

- Euclidean distance:
  $$\Large
  d(x_i, x_j)
  =
  \|x_i - x_j\|_2
  $$

- Mahalanobis distance:
  $$\Large
  d(x_i, x_j)
  =
  \sqrt{(x_i-x_j)^T \Sigma^{-1}(x_i-x_j)}
  $$

---

# K-means Model

Assume:

- Euclidean space $\mathbb{R}^D$
- Each cluster has centroid $\mu_k \in \mathbb{R}^D$
- Indicator variable $z_{ik} \in \{0,1\}$

Objective (distortion):

$$\Large
J(X, Z, \mu)
=
\sum_{i=1}^N
\sum_{k=1}^K
z_{ik}
\|x_i - \mu_k\|_2^2
$$

Goal:

$$\Large
Z^*, \mu^*
=
\arg\min_{Z,\mu}
J(X, Z, \mu)
$$

---

# Lloyd’s Algorithm

Alternate between:

### 1. Assignment Step

$$\Large
z_{ik} =
\begin{cases}
1 & k = \arg\min_j \|x_i - \mu_j\|_2^2 \\
0 & \text{otherwise}
\end{cases}
$$

### 2. Update Step

$$\Large
\mu_k
=
\frac{1}{N_k}
\sum_{i=1}^N
z_{ik} x_i
$$

where

$$\Large
N_k = \sum_{i=1}^N z_{ik}
$$

Repeat until convergence.

![[Pasted image 20260228190609.png]]

---

# K-means++ Initialization

1. Choose first centroid uniformly at random.
2. Compute:
   $$\Large
   D_i^2 = \|x_i - \mu_1\|^2
   $$
3. Choose next centroid with probability ∝ $D_i^2$.
4. Update distances to closest centroid.
5. Repeat until $K$ centroids chosen.

Improves stability.

---

# Limitations of K-means

Modeling issues:

- No probabilistic interpretation  
- Sensitive to outliers  
- Cannot detect overlapping clusters  
- No uncertainty estimates  

Algorithmic issues:

- Sensitive to initialization  

---

# Section 2 — Gaussian Mixture Models (GMM)

## Probabilistic Clustering

Model joint distribution:

$$\Large
p(x,z|\theta)
=
p(x|z,\theta)\,p(z|\theta)
$$

---

# Gaussian Mixture Model

Assume:

Cluster prior:

$$\Large
p(z|\theta) = \text{Cat}(\pi)
$$

Component distributions:

$$\Large
p(x|z_k=1,\theta)
=
\mathcal{N}(x|\mu_k,\Sigma_k)
$$

Parameters:

$$\Large
\theta = \{\pi, \mu, \Sigma\}
$$

---

# Generative Process

1. Sample cluster:
   $$\Large
   z \sim \text{Cat}(\pi)
   $$
2. Sample data:
   $$\Large
   x \sim \mathcal{N}(\mu_k, \Sigma_k)
   $$

---

# Likelihood

Marginalizing over $z$:

$$\Large
p(x|\pi,\mu,\Sigma)
=
\sum_{k=1}^K
\pi_k
\mathcal{N}(x|\mu_k,\Sigma_k)
$$

Log-likelihood:

$$\Large
\log p(X|\pi,\mu,\Sigma)
=
\sum_{i=1}^N
\log
\left(
\sum_{k=1}^K
\pi_k
\mathcal{N}(x_i|\mu_k,\Sigma_k)
\right)
$$

![[Pasted image 20260228190722.png|697]]

---

# Inference (Posterior)

Responsibilities:

$$\Large
\gamma(z_{ik})
=
p(z_{ik}=1|x_i,\pi,\mu,\Sigma)
=
\frac{
\pi_k \mathcal{N}(x_i|\mu_k,\Sigma_k)
}{
\sum_j
\pi_j \mathcal{N}(x_i|\mu_j,\Sigma_j)
}
$$

---

# Learning via EM

Maximize log-likelihood.

## E-step

Compute responsibilities:

$$\Large
\gamma_t(z_{ik})
=
\frac{
\pi_k^{(t)}
\mathcal{N}(x_i|\mu_k^{(t)},\Sigma_k^{(t)})
}{
\sum_j
\pi_j^{(t)}
\mathcal{N}(x_i|\mu_j^{(t)},\Sigma_j^{(t)})
}
$$

## M-step

$$\Large
N_k = \sum_i \gamma_t(z_{ik})
$$

Update parameters:

$$\Large
\mu_k^{(t+1)}
=
\frac{1}{N_k}
\sum_i
\gamma_t(z_{ik}) x_i
$$

$$\Large
\Sigma_k^{(t+1)}
=
\frac{1}{N_k}
\sum_i
\gamma_t(z_{ik})
(x_i - \mu_k^{(t+1)})
(x_i - \mu_k^{(t+1)})^T
$$

$$\Large
\pi_k^{(t+1)}
=
\frac{N_k}{N}
$$

Repeat until convergence.

![[Pasted image 20260228190747.png]]

---

# EM Algorithm (General)

E-step:

$$\Large
\gamma_t(Z)
=
p(Z|X,\theta^{(t)})
$$

M-step:

$$\Large
\theta^{(t+1)}
=
\arg\max_\theta
\mathbb{E}_{Z \sim \gamma_t}
[\log p(X,Z|\theta)]
$$

EM maximizes a lower bound on:

$$\Large
\log p(X|\theta)
$$

---

# Choosing Number of Clusters K

## Heuristics

- Elbow method  
- Gap statistic  
- Silhouette score  

## Probabilistic Criteria

- BIC:
  $$\Large
  \text{BIC} = M \log N - 2 \log \hat{L}
  $$
- AIC:
  $$\Large
  \text{AIC} = 2M - 2 \log \hat{L}
  $$

where $M$ = number of parameters.

---

# Hierarchical Clustering

## Agglomerative

- Bottom-up merging

## Divisive

- Top-down splitting

![[Pasted image 20260228190820.png|572]]

---

## Linkage Criteria

- Single linkage: minimum distance  
- Complete linkage: maximum distance  
- Average linkage (UPGMA)  
- Centroid linkage  
- Weighted linkage  

---

# Summary

- K-means: minimize squared distances  
- GMM: probabilistic clustering via EM  
- EM alternates:
  - Responsibilities (E-step)
  - Parameter update (M-step)
- Model selection: BIC, AIC  
- Hierarchical clustering: merge recursively  

---

# Reading

- Bishop: Chapters 9.1–9.3  
- Murphy: Chapter 11.4 (optional)