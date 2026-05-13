**Prof. Dr. Stephan Günnemann**  
Data Analytics and Machine Learning  
Technical University of Munich  
23.11.2020  

---

# 1. Introduction to Probabilistic Graphical Models (PGMs)

## Bayesian Networks

A **Bayesian Network** represents a joint distribution using a  
directed acyclic graph (DAG):

$$\Large
G = (V, E)
$$

- Each node represents a random variable.
- Directed edges often represent causal relations.
- Variables may be discrete (e.g., $\{0:\text{low}, 1:\text{high}\}$).

The graph provides:

1. A specific **factorization** of the joint distribution
   $$\Large
   p(x_1, \dots, x_{|V|})
   $$
2. A set of conditional independencies
   inferred via **d-separation**.

![[Pasted image 20260228191105.png]]

---

# 2. Bayesian Network Factorization

For a Bayesian network:

$$\Large
p(x_1, \dots, x_{|V|})
=
\prod_{n=1}^{|V|}
p\big(x_n \mid \text{Pa}(x_n)\big)
$$

where:

- $\text{Pa}(x_n)$ = set of parents of node $x_n$ in graph $G$.

---

## Example Factorization

Given a graph with nodes $x_1,\dots,x_5$:

$$\Large
p(x_1, x_2, x_3, x_4, x_5)
=
p(x_1 \mid x_4, x_5)
\cdot
p(x_2 \mid x_1, x_5)
\cdot
p(x_3 \mid x_1, x_2)
\cdot
p(x_4)
\cdot
p(x_5)
$$

This illustrates:

- Roots have no parents → unconditional factors.
- Each node depends only on its parents.

![[Pasted image 20260228192606.png]]

---

# 3. Model Parameters

The joint distribution is parameterized by:

$$\Large
\{\theta_1, \dots, \theta_{|V|}\}
$$

Each parameter:

$$\Large
\theta_n
$$

parameterizes:

$$\Large
p(x_n \mid \text{Pa}(x_n), \theta_n)
$$

In graphical notation:

- Parameters are often drawn as filled circles connected to the variable.

![[Pasted image 20260228192619.png]]

---

## Example: Parameter Tables

For the student network:

Variables:

- $D$ — Difficulty  
- $I$ — Intelligence  
- $G$ — Grade  
- $S$ — SAT score  
- $L$ — Letter  

Example conditional probability tables:

### Prior distributions

$$\Large
p(D=0)=0.5, \quad p(D=1)=0.5
$$

$$\Large
p(I=0)=0.5, \quad p(I=1)=0.5
$$

### Conditional example

$$\Large
p(G \mid D, I)
$$

(Table provided in slide 11.)

Other conditionals:

$$\Large
p(S \mid I)
$$

$$\Large
p(L \mid G)
$$

![[Pasted image 20260228192656.png]]

---

# 4. Generative Process

A Bayesian network defines a generative process:

1. Sample root variables:
   $$\Large
   D \sim p(D \mid \theta_D)
   $$
   $$\Large
   I \sim p(I \mid \theta_I)
   $$

2. Sample dependent variables:
   $$\Large
   G \sim p(G \mid D, I, \theta_G)
   $$
   $$\Large
   S \sim p(S \mid I, \theta_S)
   $$
   $$\Large
   L \sim p(L \mid G, \theta_L)
   $$

We can interpret the model as:

- A structured factorization
- A sampling procedure
- A representation of conditional independencies

![[Pasted image 20260228192713.png]]

---

# Key Concepts

- Directed acyclic graph (DAG)
- Parent set $\text{Pa}(x_n)$
- Factorization:
  $$\Large
  p(x_1,\dots,x_{|V|})
  =
  \prod_n p(x_n \mid \text{Pa}(x_n))
  $$
- Conditional independence via graph structure
- Local parameters per node
- Generative interpretation

---

# Summary

A Bayesian network:

- Compactly represents joint distributions
- Encodes conditional independence assumptions
- Factorizes joint probabilities via graph structure
- Supports generative modeling and probabilistic inference