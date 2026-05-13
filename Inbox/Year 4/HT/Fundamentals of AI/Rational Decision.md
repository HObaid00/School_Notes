## ⭐ Big Picture

Decision theory:

$$\Large
\text{Decision Theory} = \text{Probability Theory} + \text{Utility Theory}
$$

Goal of a rational agent:

$$\Large
a^* = \arg\max_a \, EU(a)
$$

---

## ⭐ Probabilistic Outcome of Actions

Random variable:

$$\Large
Result(a)
$$

Outcome probability:

$$\Large
P(Result(a)=s') = \sum_s P(s)\,P(s' \mid s,a)
$$

---

## ⭐ Utility Function

$$\Large
U(s)
$$

Expected utility:

$$\Large
EU(a) = \sum_{s'} P(Result(a)=s')\,U(s')
$$

---

## ⭐ Maximum Expected Utility (MEU)

$$\Large
a^* = \arg\max_a \sum_{s'} P(Result(a)=s')U(s')
$$

---

## ⭐ Helpful EU Identities

$$\Large
EU(x,y) = P(x,y)U(x,y)
$$

$$\Large
EU(x) = \sum_y EU(x,y)
$$

$$\Large
EU(x \mid y) = \frac{EU(x,y)}{P(y)}
$$

$$\Large
EU(x) = \sum_y P(x,y)U(x,y)
$$

---

## ⭐ Preferences

Lottery:

$$\Large
L = [p,A; (1-p),B]
$$

- $A \succ B$  
- $A \sim B$  
- $A \succeq B$  

---

## ⭐ Rational Preference Axioms

**Orderability**

$$\Large
(A \succ B) \lor (B \succ A) \lor (A \sim B)
$$

**Transitivity**

$$\Large
(A \succ B \land B \succ C) \Rightarrow (A \succ C)
$$

**Continuity**

$$\Large
A \succ B \succ C \Rightarrow \exists p: [p,A;1-p,C] \sim B
$$

**Substitutability**

$$\Large
A \sim B \Rightarrow [p,A;1-p,C] \sim [p,B;1-p,C]
$$

**Monotonicity**

$$\Large
A \succ B \Rightarrow (p>q \Leftrightarrow [p,A;1-p,B] \succ [q,A;1-q,B])
$$

**Decomposability**

$$\Large
[p,A;1-p,[q,B;1-q,C]]
\sim
[p,A;(1-p)q,B;(1-p)(1-q),C]
$$

---

## ⭐ Preferences ⇒ Utility

$$\Large
U(A) > U(B) \Leftrightarrow A \succ B
$$

Lottery utility:

$$\Large
U([p_1,s_1;\dots;p_n,s_n]) = \sum_i p_i U(s_i)
$$

Utility not unique:

$$\Large
U'(s) = aU(s) + b, \quad a>0
$$

---

## ⭐ Utility of Money

Utility is not linear in money.

$$\Large
EU(\text{Accept}) = 0.5U(s_k) + 0.5U(s_{k+2.5M})
$$

$$\Large
EU(\text{Decline}) = U(s_{k+1M})
$$

---

# Multiattribute Utility

## ⭐ Strict Dominance

$$\Large
\forall i: X_i(B) \ge X_i(A)
$$

---

## ⭐ Stochastic Dominance

$$\Large
\forall t:\int_{-\infty}^{t} p_1(x)\,dx \le \int_{-\infty}^{t} p_2(x)\,dx
$$

If $U$ monotonic:

$$\Large
\int p_1(x)U(x)dx \ge \int p_2(x)U(x)dx
$$

---

## ⭐ Additive Value Function

$$\Large
V(x_1,\dots,x_n) = \sum_i V_i(x_i)
$$

---

## ⭐ Multiplicative Utility (3 attributes)

$$\Large
U = k_1U_1 + k_2U_2 + k_3U_3
+ k_1k_2U_1U_2 + k_2k_3U_2U_3 + k_3k_1U_3U_1
+ k_1k_2k_3U_1U_2U_3
$$

---

# Decision Trees

Expected utility:

$$\Large
EU(d) = \sum_s P(s \mid d)U(s,d)
$$

Choose decision with highest EU.

---

# Value of Information (VOI)

$$\Large
VOI_e(E_j) =
\sum_k P(E_j=e_{jk}\mid e)\,MEU(\alpha_{e_{jk}}\mid e,E_j=e_{jk})
- MEU(\alpha\mid e)
$$

Property:

$$\Large
VOI_e(E_j) \ge 0
$$

---

# Decision Networks

Joint probability:

$$\Large
P(x_{1:n},d_{1:n})
=
\prod_{i=1}^n P(x_i \mid x_{1:i-1}, d_{1:i})
$$

Optimal policy:

$$\Large
\pi^*(d_i \mid x_{1:i-1}, d_{1:i-1})
=
\arg\max_{d_i} EU(d_i \mid x_{1:i-1}, d_{1:i-1})
$$

---

# ⭐ Exam Takeaways

- Rational agents maximize expected utility  
- Preferences → utility  
- Dominance simplifies choices  
- Decision trees for small problems  
- Decision networks for compact representation  
- VOI decides whether to gather information


# Rational Decisions Over Time

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
