
# ⭐ Markov Decision Processes (MDP)

## Definition

An MDP is a 5-tuple:

$$
(S, A, P, R, \gamma)
$$

- $S$ = finite set of states  
- $A(s)$ = actions available in state $s$  
- $P(s' \mid s,a)$ = transition probability  
- $R(s,a,s')$ = immediate reward  
- $\gamma \in [0,1]$ = discount factor  

---

## ⭐ Goal

Find optimal **policy** (not sequence):

$$
\pi^*(s)
$$

Optimal action maximizes expected utility:

$$
\pi^*(s) =
\arg\max_{a \in A(s)}
\sum_{s'} P(s' \mid s,a)
\left[
R(s,a,s') + \gamma U(s')
\right]
$$

---

# ⭐ Utility of State Sequences

Two coherent models:

## 1️⃣ Additive (finite horizon)

$$
U = \sum_{t=0}^{T} R(s_t,a_t,s_{t+1})
$$

## 2️⃣ Discounted (infinite horizon)

$$
U = \sum_{t=0}^{\infty} \gamma^t R(s_t,a_t,s_{t+1})
$$

If $R(s) \le R_{\max}$ and $\gamma < 1$:

$$
U \le \frac{R_{\max}}{1-\gamma}
$$

Smaller $\gamma$ ⇒ shorter effective horizon.

---

# ⭐ Utility of a State

Definition:

$$
U(s) = \text{expected discounted reward assuming optimal actions}
$$

---

# ⭐ Bellman Principle of Optimality

> An optimal policy has the property that whatever the initial state and action are, the remaining decisions must be optimal for the resulting state.

---

# ⭐ Bellman Equation (Core Exam Formula)

$$
U(s) =
\max_{a \in A(s)}
\sum_{s'} P(s' \mid s,a)
\left[
R(s,a,s') + \gamma U(s')
\right]
$$

Interpretation:

Expected future reward  
= immediate reward  
+ discounted optimal future utility

---

# ⭐ Finite-Horizon Derivation

One step:

$$
U_1(s) =
\max_a \sum_{s'} P(s' \mid s,a) R(s,a,s')
$$

Two steps:

$$
U_2(s) =
\max_a \sum_{s'} P(s' \mid s,a)
\left[
R(s,a,s') + \gamma U_1(s')
\right]
$$

General:

$$
U_i(s) =
\max_a \sum_{s'} P(s' \mid s,a)
\left[
R(s,a,s') + \gamma U_{i-1}(s')
\right]
$$

As $i \to \infty$ ⇒ Bellman equation.

---

# ⭐ Q-Function

Definition:

$$
Q(s,a)
=
\sum_{s'} P(s' \mid s,a)
\left[
R(s,a,s') + \gamma U(s')
\right]
$$

Relationship:

$$
U(s) = \max_{a} Q(s,a)
$$

Optimal policy:

$$
\pi^*(s) = \arg\max_a Q(s,a)
$$

Bellman equation for Q:

$$
Q(s,a) =
\sum_{s'} P(s' \mid s,a)
\left[
R(s,a,s') + \gamma \max_{a'} Q(s',a')
\right]
$$

---

# ⭐ Value Iteration

Idea:

Repeatedly update utilities using Bellman equation.

Algorithm:

- Initialize $U(s)=0$ (terminal states fixed)
- Repeat:

$$
U(s) \leftarrow
\max_{a}
\sum_{s'} P(s' \mid s,a)
\left[
R(s,a,s') + \gamma U(s')
\right]
$$

until convergence.

---

## ⭐ Convergence (Important)

Max norm:

$$
\|U\|_\infty = \max_s |U(s)|
$$

Contraction:

$$
\|U_{i+1} - U^*\|
\le
\gamma \|U_i - U^*\|
$$

⇒ converges if $\gamma < 1$.

Stopping condition:

If

$$
\|U_{i+1} - U_i\| < \varepsilon
$$

then error is bounded by:

$$
\frac{2\varepsilon \gamma}{1-\gamma}
$$

---

# ⭐ Policy Iteration

Two alternating steps:

## 1️⃣ Policy Evaluation

Given policy $\pi$:

$$
U^\pi(s)
=
\sum_{s'}
P(s' \mid s,\pi(s))
\left[
R(s,\pi(s),s') + \gamma U^\pi(s')
\right]
$$

(No max ⇒ linear equations)

---

## 2️⃣ Policy Improvement

$$
\pi_{\text{new}}(s)
=
\arg\max_a
\sum_{s'}
P(s' \mid s,a)
\left[
R(s,a,s') + \gamma U^\pi(s')
\right]
$$

Repeat until policy unchanged.

---

## ⭐ Comparison

- Value Iteration: simpler, often faster
- Policy Iteration: fewer iterations, stronger guarantees
- Both converge to optimal policy

---

# ⭐ MDP vs POMDP

Fully observable:

$$
\text{MDP} = \text{Markov chain} + \text{actions} + \text{rewards}
$$

Partially observable:

$$
\text{POMDP} = \text{HMM} + \text{actions} + \text{rewards}
$$

(Not exam-relevant in detail)

---

# ⭐ Exam Essentials Checklist

- MDP definition $(S,A,P,R,\gamma)$
- Difference: optimal sequence vs optimal policy
- Discounted utility formula
- Bellman equation
- Q-function definition
- Value iteration update rule
- Convergence condition ($\gamma < 1$)
- Policy evaluation vs policy improvement
- Difference MDP vs POMDP

---

# ⭐ One-Line Summary

MDPs model sequential decision-making under uncertainty; optimal policies are computed via the Bellman equation using value iteration or policy iteration.
