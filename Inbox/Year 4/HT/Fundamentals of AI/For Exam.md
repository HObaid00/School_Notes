
---
## Search
5 components:
* Initial State
* Actions
* Transition-model
* Goal test
* Cost

Tree Search: Revisiting nodes is possible -> good space complexity

Graph Search: Explored Set, Revisiting nodes is not possible -> good time complexity

Total Search Cost function 
$$\Large
f(n) = g(n) \ + \ h(n)
$$
Where 
$$\Large
\begin{array}
gg(n) = \text{heuristic for cost so far}\\
h(n) = \text{heuristic for possible upcoming costs}
\end{array}
$$

A heuristic $h(n)$ is **admissible** if it **never overestimates** the true cost to reach the goal. 

Meaning: 
	It can be **too optimistic (too low)**, but **never too pessimistic** (**too high**). 

For search questions you need to put up a table of:
* Expanded Node - The Node we are viewing through. List Node and cost so far: $\{A, g(n)\}$
* Frontier Nodes - Seen Nodes yet to be explored. List Node and cost to go to Node: $\{B, h(n)\}$
* Explored Nodes - List of Nodes we have already visited and total cost had to pay to get there: $\{C, f(n)\}$
---
### Uninformed Search

| Criterion | BFS            | UCS                             | DFS         | DLS         | IDS            |
| --------- | -------------- | ------------------------------- | ----------- | ----------- | -------------- |
| Complete  | $\text{Yes}^a$ | $\text{Yes}^{a, b}$             | $\text{No}$ | $\text{No}$ | $\text{Yes}^a$ |
| Optimal   | $\text{Yes}^c$ | $\text{Yes}$                    | $\text{No}$ | $\text{No}$ | $\text{Yes}^c$ |
| Time      | $O(b^d)$       | $O(b^{1+\frac{c^*}{\epsilon}})$ | $O(b^m)$    | $O(b^l)$    | $O(b^d)$       |
| Space     | $O(b^d)$       | $O(b^{1+\frac{c^*}{\epsilon}})$ | $O(b*m)$    | $O(b*l)$    | $O(b*d)$       |
$$\Large
\begin{array}
a\text{a: if b is finite} \qquad \text{b: broading factor} \\
\text{b: if all step cost } \geq \epsilon \qquad \text{d: depth of goal} \\
\text{c: all step cost are identical} \qquad \text{m: deepest node} \\
\end{array}
$$
#### Bidirectional Search
One goal must be well defined. 
$\Large b^\frac{d}{2} + b^\frac{d}{2} < b^d$ actions must be reversible

---
### Informed Search 

#### Greedy First Search (GFS):
$f(n) + g(n) + h(n)$ is non-negative and $h(goal) = 0$. Is Complete for graph search, for tree search not optimal, Time & Space Complexity $O(b^m)$

#### A*-Search:
$$\Large
f(n) = g(n) \ + \ h(n)
$$
Tree Search: $h(n)$ admissible: $h(n) \leq g(n, goal)$ 
Graph Search: $h(n)$ consistent: $\forall n \ h(n) \leq c(n, n') + h(n')$

---
## Logical Equivalence:
$$\Large
\begin{array}
a \alpha \ \land \ (\beta \ \lor \ \gamma) \equiv
(\alpha \ \land \beta) \ \lor \ (\alpha \ \land \ \gamma) \\

\alpha \ \lor \ (\beta \ \land \ \gamma) \equiv 
(\alpha \ \lor \ \beta) \ \land \ (\alpha \ \lor \ \gamma) \\

\neg(\alpha \ \land \ \beta) \equiv \neg\alpha \ \land \ \neg\beta , \quad
\neg(\alpha \ \lor \ \beta) \equiv \neg\alpha \ \lor \ \neg\beta \\

\alpha \ \Rightarrow \beta \equiv \neg \alpha \ \lor \ \beta \\
\alpha \ \iff \beta \equiv (\alpha \ \Rightarrow \beta) \land (\beta \ \Rightarrow \alpha) \\

\text{Entailment: } \alpha \ \models \beta \ \text{iff} \ M(\alpha) \ \leq \ M(\beta) \\



\text{Validity: } \alpha \text{ is valid iff } \alpha \equiv True \\
\text{Unsatisfiable: } \alpha \text{ is unsatisfiable iff } \alpha \equiv False \\

\text{Skolemization: } \forall\alpha \ \exists\beta \ P(\alpha, \ \beta) \equiv \ P(\alpha, f(\alpha))


\end{array}
$$

Conversion to CNF:
* Eliminate $\iff$ and $\Rightarrow$
* Move $\neg$ inwards 
* Skolemization -> get rid of $\exists$
* Drop $\exists$
* Distribute $\land$ or  $\lor$

---
## Constraint Satisfaction Problem
$$\Large
\text{CSP} : \text{Tuple}\{X, D, C\}
$$
Goal: Assign a value to each variable such that all core slots.
Conved n-Ary constraint  into binary :
1. Replace constraint by new variable Z will domain of Z as a n-Tuple, which is restricted to sohistic constraint e.g
$$\Large
\text{dom}(Z) = \{(z_1, z_2 , z_3) \ | \ z_1 + z_2 + z_3 \ \land \ z_1 \in \text{dom}(A), z_2 \in \text{dom}(B), z_3 \in \text{dom}(C) \}
$$
2. Introduce new binary constraint to match the values of $Z$ with the neighboring variables $(\text{fst}(z) = A)$

---
## Backtracking Search:

**Variables Selection:** 
* Minimum Remaining Values: choose variable
* Degree Heuristic: choose variable involved in highest number of constraints (highest degree)

**Value Selection:**
* Least Constraining Value: choose value that rules out the fewest choices for neighboring values

**Inference Technique:**
* **Forward Checking:** inconsistent values of neighboring variables are removed (after each assignment)
* **Arc Consistency algorithm:** after each assignment or preprocessing: 
	* inconsistent values of all variables are removed
	* after assigning variables $X_j$ add each arc $(X_i,X_j)$ to queue
	* preprocessing: add all arcs to queue if remove_inconsistent $(X_i, X_j)$ then if size of Domain $(X_i) = 0$ -> $\{return failure\}$ for each $X_K$ in Neighbors $[X_i]/\{X_j\}$ 

---

## Inference Propositional Logic
* Forward-and Backward Chaining (Only Horn Clause)
* Resolution (Only CNF)

**Horn Clause:** symbol or (conjunction) $\Rightarrow$ symbol:
- [v] $\alpha$
* [v] $(\alpha \ \land \ \beta) \ \Rightarrow \ (...)$
* [ ] $(\alpha \ \lor \ \beta) \ = \ (...)$

**Resolution:** $\text{KB} \$
* 