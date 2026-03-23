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
