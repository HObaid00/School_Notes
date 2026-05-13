
---

## 📘 Probability & Bayesian Inference

Likelihood (i.i.d.):
$$  
\Large   
p(D | \theta) = \prod_{i=1}^{N} p(x_i | \theta)  
$$
Posterior (Bayes Rule):
$$  
\Large   
p(\theta | D) \propto p(D | \theta) p(\theta)  
$$


Marginal Likelihood (Evidence):
$$
\Large
p(D | a,b) = \int p(D | \theta)\, p(\theta | a,b)\, d\theta
$$


MAP Estimate
$$
\Large
\theta_{\text{MAP}} = \arg\max_\theta \; p(D | \theta)\, p(\theta)
$$


MLE Estimate
$$  
\Large  
\theta_{\text{MLE}} = \arg\max_\theta ; p(D | \theta)  
$$


Uniform MLE
$$  
\Large  
b_{\text{MLE}} = \max_i x_i  
$$


Pareto Update
$$  
\Large  
\lambda_{\text{new}} = \max(x_1, ..., x_N, \lambda), \quad  
\alpha_{\text{new}} = N + \alpha  
$$

---

## 📘 Distributions


Gaussian - Normal Distribution
$$  
\Large  
\mathcal{N}(x | \mu, \sigma^2) =  
\frac{1}{\sqrt{2\pi\sigma^2}}  
\exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)  
$$
Bernoulli
$$  
\Large  
\text{Bern}(x|\theta) = \theta^x (1-\theta)^{1-x}  
$$

Uniform
$$  
\Large  
p(x | b) =  
\begin{cases}  
	\frac{1}{b}, & 0 \le x \le b \\  
	0, & \text{otherwise}  
\end{cases}  
$$

Gamma
$$  
\Large  
p(\lambda | a, b) =  
\frac{b^a}{\Gamma(a)} \lambda^{a-1} e^{-b\lambda}  
$$
Exponential Likelihood
$$  
\Large  
p(x | z) = 2^z \exp(-x 2^z)  
$$

---

## 📘 Linear Regression & Optimization

OLS Solution
$$  
\Large  
w^* = (X^T X)^{-1} X^T y  
$$
Ridge Solution
$$  
\Large  
w^* = (X^T X + \lambda I)^{-1} X^T y  
$$

Prediction
$$  
\Large  
\hat{y} = w^T x  
$$
Regularized Loss
$$  
\Large
\min_w ; \frac{1}{2} \sum_{i=1}^{N} (w^T x_i - y_i)^2 + \frac{\lambda}{2} w^T w  
$$

Log-Likelihood
$$  
\Large    
\log p(D | w) = \sum_{i=1}^{N} \log p(y_i | x_i, w)  
$$

---

## 📘 Ridge Regression Trick

$$  
\Large  
\text{Bias Solution} \  
w_{D+1} = \frac{1}{N + \lambda} \sum_{i=1}^{N} y^{(i)}  
$$

$$  
\Large  
\text{Centered Targets} \  
\tilde{y}^{(i)} =  
y^{(i)} - \frac{1}{N + \lambda} \sum_{j=1}^{N} y^{(j)}  
$$

---

## 📘 Logistic Regression

Sigmoid:
$$  
\Large  
\sigma(z) = \frac{1}{1 + e^{-z}}  
$$
Model:
$$  
\Large  
f(x, w) = \sigma(w^T x)  
$$
Logistic Loss:
$$  
\Large  
L(w) =

- \sum_{i=1}^{N}  
    \left[  
    y_i \log \sigma(w^T x_i)
    

- (1-y_i)\log(1-\sigma(w^T x_i))  
    \right]
    
- \frac{\lambda}{2} w^T w  
    $$

Gradient:

$$  
\Large  
\nabla_w L =

- \sum_{i=1}^{N} x_i (y_i - \sigma(w^T x_i))
    

- \lambda w  
    $$

---

## 📘 Distance Metrics

$L_1$ Distance
$$  
\Large  
|x^{(1)} - x^{(2)}|_1 =  
\sum_i |x_i^{(1)} - x_i^{(2)}|  
$$
$L_2$ Distance
$$  
\Large  
|x^{(1)} - x^{(2)}|_2 =  
\sqrt{\sum_i (x_i^{(1)} - x_i^{(2)})^2}  
$$


$L_∞$ Distance
$$  
\Large  
|x^{(1)} - x^{(2)}|_\infty =  
\max_i |x_i^{(1)} - x_i^{(2)}|  
$$

---

## 📘 Decision Trees

Squared Error:
$$\Large
e(Y) = \sum_{y_i \in Y} (y_i - \bar{y})^2
$$
Mean in Leaf:
$$\Large
\bar{y} = \frac{1}{|Y|}\sum_{y_i \in Y} y_i
$$

### Entropy:
$$  
\Large  
H(y) = - \sum_{c} p(y=c)\log p(y=c)  
$$

Information Gain
$$  
\Large  
\Delta = H(y) - \sum_k p_k H(y | x=k)  
$$

Gini Index:
$$  
\Large  
i_G(t) = 1 - \sum_{i \in C} \pi_i^2  
$$
Miss classification:
$$  
\Large    
i_E(t) = 1 - \max_c p(y=c|t)  
$$
---

## 📘 Gaussian Posterior

Posterior Gaussian
$$  
\Large  
p(x_0 | x_1) =  
\mathcal{N}\left(x_0 \mid \frac{1}{2}x_1, \frac{1}{2}I\right)  
$$

---

## 📘 Optimization

Projection
$$
\Large
\pi_X(x) =
\begin{cases}
(\min(1,\max(0,x_1)), \min(1,\max(0,x_2))) & x \in X_0 \\
\frac{x}{\|x\|_2} & x \in X_1 \\
x & x \in X
\end{cases}
$$

Max on Sphere

$$  
\Large  
\max_{x:|x|_2=1} c^T x = |c|_2  
$$

---
## 📘 Convexity
### 1. Definition
A set $\Large X$ is **convex** if:
	For any two points $x, \ y \in X$, every point on the line between them is also in $\Large X$.
Mathematically:
$$\Large
\forall x,y \in X, \ \forall\lambda \in [0, 1]:\quad \lambda x +(1-\lambda)y \in X
$$

### 2. Geometric intuition
Think:
* Pick any two points in the set
* Draw a straight line between them
* If the entire line stays inside the given area -> **convex**
If the line "leaves" the area -> **not convex**

### 3. Examples

**Convex sets**
* A solid circle / sphere
* A square / cube
* A Triangle
* A line segment
-> These have no "dents"

**Not Convex**
* A crescent shape
* A donut shape (hole inside)
* Anything with a "cave" or indentation
### 4. Useful Rules 
Shortcuts for quick implementation

#### Rule 1: Intersection preserves convexity
if $\Large A$ and $\Large B$ are both convex, then:
$$\Large
A \ \cap \ B \text{ is convex}
$$

#### Rule 2: Norm balls are convex
$$\Large
\{x \ : \ || x ||_2 \leq 1\}
$$
is convex

#### Rule 3: Linear constraints are convex
Sets like:
$$\Large
x_i \ \geq 0, \quad Ax \leq b
$$
are convex

#### Rule 4: Convex combinations stay inside
if $x, y \ \in X$ then:
$$\Large
\lambda x + (1-\lambda) y \in X
$$
This is just the definition again, but often used directly in proofs.

#### Rule 5: Affine sets are convex
Anything like:
$$\Large
Ax = b
$$
is convex.

--- 



## 📘 Kernels

Polynomial Kernel: 
$$  
\Large    
k(x_1, x_2) = (x_1^T A x_2 + 1)^p  
$$
Kernel Definition:
$$\Large
k(x, y) = \phi(x)^T\phi(y)
$$
Valid kernel operations: 
* Sum of kernels
* Product of kernels
* Positive scalar multiple
* Feature map composition

Geometric series:
$$\Large
\frac{1}{1- r} = \sum_{k=0}^\infty r^k
$$

---

## 📘 Naive Bayes

Naive Bayes
$$  
\Large   
p(y|x) \propto p(x_1|y), p(x_2|y)\cdots p(y)  
$$

Categorical Prior
$$  
\Large   
y \sim \text{Categorical}(\pi)  
$$


Gaussian Class Conditional
$$  
\Large  
x | y=c \sim \mathcal{N}(\mu_c, \sigma^2)  
$$


Bernoulli Class Conditional
$$  
\Large  
x | y=c \sim \text{Bernoulli}(\alpha_c)  
$$

---

## 📘 Markov Models


Likelihood
$$  
\Large    
L = \prod_{i,j} p_{i,j}^{n_{i,j}}  
$$

Log-Likelihood
$$  
\Large
\log L = \sum_{i,j} n_{i,j} \log p_{i,j}  
$$
---
## K-means 

### 1. State the assignment rule
Each point is assigned to the nearest centroid:
$$\Large
c(x)=\arg\min_j \|x-\mu_j\|_2
$$

### 2. Compare distances
For any point $x$ in cluster $X_i$:
- distance to its own centroid: bound it from above
- distance to other centroids: bound it from below

Typical form:
$$\Large
\|x-\mu_i\|_2 \le a
\quad\text{and}\quad
\|x-\mu_j\|_2 > a \quad (j\neq i)
$$

Therefore $x$ is assigned to $\mu_i$.

### 3. Argue the update step
The updated centroid is the mean of the assigned points:
$$\Large
\mu_i^{new}=\frac{1}{|X_i|}\sum_{x\in X_i} x
$$

If all assigned points lie in a convex set, then the mean also lies in that set.

Therefore the centroid stays in the same region / cluster ball.

### 4. Conclude convergence or correctness
Since assignments are correct and the updated centroids remain in the same regions, the assignments do not change in the next iteration.

Hence K-means recovers the intended clustering and terminates.

For any $x\in X_i$, we show that $x$ is closer to $\mu_i$ than to any other centroid $\mu_j$.
Using the assumptions, we derive
$$\Large
\|x-\mu_i\|_2 \le a
\quad\text{and}\quad
\|x-\mu_j\|_2 > a \ \text{for all } j\neq i.
$$
Hence every point in $X_i$ is assigned to centroid $\mu_i$.

After the assignment step, each centroid is updated as the mean of the points assigned to it. Since these points all lie in the same convex region, the updated centroid remains in that region. Therefore the same distance argument still applies in the next iteration, so the assignments do not change anymore.

Thus K-means recovers the desired clustering and converges.

Take any $x\in X_i$.
Then $\|x-\mu_i\| \le \dots$.
For every $j\neq i$, $\|x-\mu_j\| > \dots$.
So $x$ is assigned to $\mu_i$.

The centroid update is an average of points in $X_i$, so by convexity it stays in the same region.
Thus assignments remain unchanged, and K-means converges to the correct clustering.