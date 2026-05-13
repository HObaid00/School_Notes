#### Why Probabilistic Reasoning?
* Logic alone fails under **uncertainty**
* We use **degrees of belief** -> probabilities
* Goal: Minimize **expected cost** when acting under uncertainty
Probabilities subsume uncertainty form incomplete or unreliable knowledge.
#### Probability Space
* Sample Space: $\Large \Omega$ = set of outcomes
* Event space: F = power-set of $\Large \Omega$
* Probability function P:

$$\Large
P(e) \geq 0
$$
$$\Large
\sum_{\omega \in \Omega}P(\omega)=1
$$
$$\Large
P(e_1 \cup e_2) = P(e_1) + P(e_2) \quad (if \space e_1,\space e_2 \space mutually \space exclusive)
$$
#### Random Variables
Function:
$$\Large
X:\Omega \rightarrow D
$$
Example:
$$\Large
X(heads) = 1, \space X(tails) = 2
$$
#### Expectation
$$\Large
E(X) = \sum_{x \in D_X} x P(X=x)
$$
Example (fair die):
$$\Large
E(X) = \sum_{x = 1}^6 i \frac{1}{6} = 3.5
$$
#### Joint & Marginal Probability
Joint:
$$\Large
P(X=x,Y=y)
$$
Marginalization:
$$\Large
P(X=x) = \sum_y P(X=x,Y=y)
$$
#### Conditional Probability
$$\Large
P(X, Y) = \frac{P(X,Y)}{P(Y)}
$$

#### Bayes' Rule
$$\Large
P(X, Y) = \frac{P(X|Y)P(Y)}{P(Y)}
$$
Expanded:
$$\Large
P(X, Y) = \frac{P(X|Y)P(Y)}{\sum_y P(X, y)P(y)}
$$
#### Independence
$X$ and $Y$ independent iff:
$$\Large
P(X, Y) = P(X)P(Y)
$$
Equivalent:
$$\Large
P(X|Y) = P(X)
$$
#### Bayesian Network Definition
A BN is a **directed acyclic graph (DAG)**:
* Node = random variable
* Edge = direct dependency
* Each node $X_i$ has CPT:
$$\Large
P(X_i | Parents(X_i))
$$
#### Semantics of BN
$$\Large
P(x_1, ... , x_n) = \prod_{i = 1}^n P(x_i | Parents(X_i))
$$
#### Compactness
If each node has $\le k$ parents:
$$\Large
O(n \cdot 2^k) \qquad vs \qquad O(2^n)
$$
for full joint distribution.

#### Independence Patterns
1. - Chain: $X \rightarrow E \rightarrow Y$
    - $X \perp Y \mid E$
- Fork: $X \leftarrow E \rightarrow Y$    
    - $X \perp Y \mid E$
- Collider: $X \rightarrow E \leftarrow Y$
    - $X \perp Y$
    - $X \not\perp Y \mid E$

## Inference in Bayesian Networks
#### Goal
Compute:
$$\Large
P(Query | Evidence)
$$
#### Inference by Enumeration
$$\Large
P(Q|E) = \alpha \sum_H \prod_i P(x_i | Parents(X_i))
$$
* $H$ = hidden variables
* $\alpha$ = normalization constant

#### Variable Elimination (VE)
Steps:
1. Create factors
2. Multiply factors containing same variable
3. Sum out hidden variables
4. Normalize

#### Factor Product
If $f_1(A,B)$ and $f_2(B,C)$:
$$\Large
f_3(A,B,C) =f_1(A, B) \times f_2(B,C)
$$
#### Summing Out
$$\Large
f(A,B) = \sum_c f(A, B, C)
$$
#### Variable Ordering
Choose elimination order minimizing intermediate factor size.

#### Variable Relevance
Remove any lead node not in:
* Query
* Evidence

#### Complexity
Exact inference is **NP-hard**.
## Approximate Inference
#### Direct Sampling
Generate samples from:
$$\Large
P(x_1, ..., x_n) = \prod_i P(x_i | Parents(X_i))
$$
Estimate probabilities by frequency.
Not suitable for conditional probabilities.

#### Rejection Sampling
Estimate:
$$\Large
\hat{P}(X | e)=\frac{N(X,e)}{N(e)}
$$
Inefficient if $P(e)$ is small.

#### Likelihood Weighting
Fix evidence variables.
Weight each sample:
$$\Large
\omega = \prod_i P(e_i | Parents(E_i))
$$
#### Consistency
As $N \rightarrow \infty$
$$\Large
\hat{P}(X| e) \rightarrow P(X, e)
$$
## Final Summary
* BNs encode conditional independence
* Bayes' rule central
* Exact inference: Enumeration, VE
* Approximate inference: Direct, Rejection, Likelihood Weighting

