#### Big Picture
* Models **sequential stochastic processes** with hidden state.
* Extends Markov chains with **sensor (observation) uncertainty.**
* Assumes:
	* Markov property
	* Stationary
	* Discrete time
#### Stochastic & Markov Processes
**Stochastic process**
A sequence of random variables:
$$\Large
X_1, X_2, X_3, ...
$$
**Markov Property**:
$$\Large
P(X_n = x_i | X_{n-1}, ..., X_0) \equiv P(X_n = x_i | X_{n-1})
$$
**Stationary Markov Process**
$$\Large
P(X_n =x_i | X_{n-1} = x_j) = P(X_{n+t} = x_i | X_{n-1+t} = x_j)
$$
#### Stationary Markov Chain
Law of total probability:
$$\Large
P(X_n = x_i) = \sum_{j=1}^N P(X_n = x_i | X_{n-1} = x_j)P(X_{n-1} = x_j)
$$
Matrix form:
$$\Large
\mathbf{p}_n = T\mathbf{p}_{n-1}
$$
Where
$$\Large
(T)_{i,j} = P(X_n = x_i | X_{n-1} = x_j)
$$
Iterated:
$$\Large
\mathbf{p}_n = T^n \mathbf{p}_0
$$
#### Sensor Model
Observation depend only on current state:
$$\Large
P(E_t | X_{0:t}, E_{0:t-1}) = P(E_t | X_t)
$$
#### Hidden Markov Model Definition
An HMM consists of:
* State transition model:
$$\Large T_{i,j} = P(X_t = x_i | X_{t-1} = x_j)$$
* Sensor (emission) model:
$$\Large H_{i,j} = P(E_t = e_i | X_t = x_j)$$
* Belief state:

Update equations:
$$\Large
\mathbf{p}_t = T\mathbf{p}_{t-1}
$$
$$\Large
\hat{\mathbf{p}}_t = H\mathbf{p}_t
$$
#### Joint Probability of HMM
Given prior $P(X_0)$:
$$\Large
P(X_{0:t}, E_{1:t}) = (\prod_{i=1}^t P(E_i | X_i)P(X_i | X_{i-1}))P(X_0)
$$
## Inference Tasks
#### Prediction 
$$\Large
P(X_{t+k+1}|e_{1:t}) = \sum_{x_{t+k}}P(X_{t+k+1} | x_{t+k})P(x_{t+k}|e_{1:t})
$$
As $k \to \infty$, converges to stationary distribution.

#### Filtering (Belief Update)
Recursive form:
$$\Large
P(X_{t+1} | e_{1:t+1}) =\alpha P(e_{t+1} | X_{t+1}) \sum_{x_i} P(X_{t+1} | x_t) P(x_t | e_{1:t})
$$
Matrix form:
$$\Large
\mathbf{f}_{t:t+1} = \alpha O_{t+1} T \mathbf{f}_{1:t}
$$
#### Smoothing
Compute past state using future evidence:
$$\Large
P(X_k | e_{1:t}) = \alpha f_{1:k} \times b_{k+1:t}
$$
Backward recursion:
$$ \Large
b_{k+1:t} = T^T O_{k+1}b_{k+2:t}
$$
#### Most Likely Explanation (Viterbi)
Goal:
$$\Large
\arg\max_{x_{1:t}} P(x_{1:t}|e_{1:t})
$$
Recursive form:
$$\Large
\delta_{t+1}(x_{t+1})=P(e_{t+1}|x_{t+1})\max_{x_i}[P(x_{t+1}|x_t)\delta_t(x_t)]
$$
Store backpoints -> backtrack for optimal sequence

## Approximate Inference
#### Particle Filtering
Monte Carlo approximation.

Steps:
 1. **Propagate**
 2. **Weight**
$$\Large \omega_i=P(e_t|x_t^{(i)})$$
 3. **Resample**
Consistency:
$$\Large
\hat{P}(X_t|e_{1:t}) \rightarrow P(X_t|e_{1:t}) \space as \space N \rightarrow \infty
$$

## Complexity
* Prediction, Filtering, Smoothing, Viterbi:
$$\Large O(t)$$
* Particle filtering:
$$\Large O(N)$$

## Exam Checklist
* Markov property
* HMM components $(T, H, P(X_0))$
* Filtering equation
* Prediction vs Smoothing
* Viterbi recursion
* Difference: filtering vs most-likely explanation
* Particle filtering steps