# ⭐ What is Learning?

An agent is learning if it **improves its performance on future tasks** after making observations.

Motivation:
- Designers cannot anticipate all situations
- Environments change
- Some problems hard to hand-code (e.g., vision)

---

# ⭐ Types of Learning

## Unsupervised Learning
- No labeled outputs
- Finds structure/patterns
- Example: clustering

## Supervised Learning
- Learn mapping from input to output

## Reinforcement Learning
- Learn from rewards/punishments

---

# ⭐ Supervised Learning

Training set:

$$
(x_1,y_1),(x_2,y_2),\dots,(x_N,y_N)
$$

Unknown target function:

$$
y = f(x)
$$

Goal: find hypothesis

$$
h \approx f
$$

---

## Hypothesis Selection (MAP)

$$
h^* = \arg\max_{h\in H} P(h \mid data)
$$

Using Bayes rule:

$$
h^* = \arg\max_{h\in H} P(data \mid h)P(h)
$$

- Prefer **simple hypotheses** (Ockham’s Razor)
- Use **test set** for generalization

---

# ⭐ Decision Trees

- Tree represents a Boolean function
- Internal node: test attribute  
- Edge: attribute value  
- Leaf: output (True/False)

Decision trees can express **any Boolean function**.

---

## Expressiveness

For $n$ Boolean attributes:

$$
2^n \text{ rows in truth table}
$$

$$
2^{2^n} \text{ possible Boolean functions}
$$

Prefer **compact trees** to generalize.

---

# ⭐ Entropy (Information Theory)

Entropy of variable $V$:

$$
H(V) = -\sum_k P(v_k)\log_2 P(v_k)
$$

Binary entropy:

$$
B(q) = -(q\log_2 q + (1-q)\log_2(1-q))
$$

If training set has $p$ positives and $n$ negatives:

$$
H(\text{goal}) = B\left(\frac{p}{p+n}\right)
$$

---

# ⭐ Remainder

Attribute $A$ with values $v_1,\dots,v_d$:

$$
Remainder(A) =
\sum_{k=1}^d
\frac{p_k+n_k}{p+n}
B\left(\frac{p_k}{p_k+n_k}\right)
$$

---

# ⭐ Information Gain

$$
Gain(A) =
B\left(\frac{p}{p+n}\right) - Remainder(A)
$$

Choose attribute with **maximum gain**.

---

# ⭐ Decision Tree Learning Algorithm

1. If examples empty → return plurality value  
2. If all same classification → return class  
3. If no attributes → return plurality value  
4. Else:
   - Choose

$$
A = \arg\max_a Gain(a)
$$

   - Split on $A$ and recurse

---

# ⭐ Reinforcement Learning (RL)

Agent interacts with environment:

- Observes state $s$
- Chooses action $a$
- Receives reward $r$

---

## Policy

Deterministic:

$$
\pi : S \rightarrow A
$$

Stochastic:

$$
\pi(a,s) \in [0,1], \quad \sum_a \pi(a,s)=1
$$

---

## Objective

Maximize expected utility:

$$
\max_{\pi} U^\pi(s)
$$

Value function:

$$
U^\pi(s) =
\sum_{a}\pi(a,s)
\sum_{s'}
P(s' \mid s,a)
\left[ R(s,a,s') + \gamma U^\pi(s') \right]
$$

Optimal:

$$
U^*(s)=
\max_a
\sum_{s'}
P(s' \mid s,a)
\left[ R(s,a,s') + \gamma U^*(s') \right]
$$

---

# ⭐ Q-Function

$$
Q^\pi(s,a)=
\sum_{s'}
P(s' \mid s,a)
\left[
R(s,a,s')+
\gamma
\sum_{a'}
\pi(s',a')Q^\pi(s',a')
\right]
$$

Optimal:

$$
Q^*(s,a)=
\sum_{s'}
P(s' \mid s,a)
\left[
R(s,a,s')+
\gamma \max_{a'} Q^*(s',a')
\right]
$$

Policy:

$$
\pi^*(s)=\arg\max_a Q^*(s,a)
$$

---

# ⭐ Q-Learning (Model-Free)

Incremental update:

$$
Q_{i+1}(s,a)
=
Q_i(s,a)
+
\alpha
\left[
R(s,a,s')+
\gamma \max_{a'} Q_i(s',a')
-
Q_i(s,a)
\right]
$$

- $\alpha$ = learning rate  
- Bracket term = **TD error**

---

# ⭐ Exploration vs Exploitation

- Exploration: try random actions  
- Exploitation: use best-known action  
- Need balance

---

# ⭐ On-Policy vs Off-Policy

- On-policy: learn using same policy as acting  
- Off-policy: learn about different target policy  

Q-learning is **off-policy**.

---

# ⭐ RL Algorithm Classes

- Model-based vs Model-free  
- Policy optimization vs Q-learning  

(Details of deep RL not exam relevant)

---

# ⭐ Exam Takeaways

- Difference between learning types  
- Supervised learning equation  
- MAP hypothesis selection  
- Entropy & information gain  
- Decision tree learning steps  
- RL value function & Bellman form  
- Q-learning update rule  
- Exploration vs exploitation  

---

# ⭐ One-Line Summary

Learning enables agents to improve from data; supervised learning fits functions, decision trees use entropy-based splitting, and reinforcement learning learns optimal behavior from reward.
