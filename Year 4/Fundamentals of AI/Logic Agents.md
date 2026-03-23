## Knowledge Based Agents
Knowledge Base (KB):
* A knowledge base is a set of sentences in a formal language
* Contains domain-specific knowledge
Inference Engine:
* Applies domain-independent algorithms
* Derives new knowledge from the KB
Why agents  acquire knowledge:
* Inference: Derive new facts from existing ones
* Declarative input: Knowledge added externally
* Perception: Knowledge from sensors
Level of description
* Knowledge level: what the agent knows
* Implementation level: Data structures + algorithms

## Basics of Logic
Syntax:
* Rules for forming well-formed sentences
* Ex: $x+y=4$ not $x4y=$
Semantics:
* Defines meaning/truth conditions
* A sentence is true or false under given assignment
Model:
* A model assigns truth values to symbols
* Used to evaluate sentences

## Satisfaction and Entailment
Satisfaction:
* A model $m$ satisfies a sentence $\alpha$ if $\alpha$ is true in $m$
* $M(\alpha) =$ set of all models where $\alpha$ is $true$
Entailment:
* $\alpha$ entails $\beta$ -> ( $\alpha \models \beta$ ) if: $M(\alpha) \subseteq M(\beta)$
* Meaning whenever $\alpha$ is $true$, $\beta$ must also be $true$
Critical Section:
* Entailment $\neq$ Implication
* Implication is a sentence
* Entailment is a relationship between sentences

## Propositional Logic 
#### Syntax
* Symbols: Atomic Sentences
* Local connectives and Operator precedence (high -> low):
	1. $\neg$ (negation)
	2. $\land$ (and)
	3. $\lor$ (or)
	4. $\implies$ (implication)
	5. $\iff$ (bi-conditional)

#### Truth Evaluations Rules
* $\neg S = true$ if $S = false$
* $S_1 \land S_2 = true$ if both $S_1, S_2 = true$
* $S_1 \lor S_2 = true$ if either $S_1, S_2 = true$
* $S_1 \implies S_2$ is $false$ only if $S_1 = true$ and $S_2 = false$
* $S_1 \iff S_2$ is $true$ if both have the same value

#### Truth Tables
* Must be able to construct and in interpret
* Especially important: $\implies$ (implication)

## Inference by Enumeration
Idea:
* Enumerate all models
* Check if $\alpha$ is true in every model where KB is $true$
Properties:
* Time $O(2^n)$
* Space $O(n)$
* Conceptually simple computationally expensive
Exam Note:
* Concept only
* Understand why it works and why its inefficient

## Propositional Theorem Proving
* Logical equivalence: $\alpha \equiv \beta$ if $\alpha \models \beta \space \& \space \beta \models \alpha$
* Validity ($\forall$): Sentence $true$ in all models (tautology)
* Satisfiability ($\exists$):
	* Sentence is true in some model
	* SAT problem is NP-complete

## Inference Rules
#### Core Rules
***Modus Ponens***:   $\Huge \frac{\alpha \implies \beta , \qquad \alpha}{\beta}$  
* Meaning that when ${\Large \alpha \implies \beta}$  and $\Large \alpha$ is given, $\Large \beta$ can be inferred.

***AND***-Elimination:   $\Large \alpha \land \beta \implies \alpha$ 


#### Logical Equivalence (Recognize and Apply)

$\Large (\alpha \land \beta) \equiv (\beta \land \alpha)$ commutativity of $\Large \land$

$\Large (\alpha \lor \beta) \equiv (\beta \lor \alpha)$ commutativity of $\lor$

$\Large ((\alpha \land \beta) \land \gamma) \equiv (\alpha \land (\beta \land \gamma))$ associativity of $\Large \land$

$\Large ((\alpha \lor \beta) \lor \gamma) \equiv (\alpha \lor (\beta \lor \gamma))$ associativity of $\Large \lor$

$\Large \neg(\neg \alpha) \equiv \alpha$ Double-Negation elimination

$\Large (\alpha \Rightarrow \beta) \equiv (\neg \beta \Rightarrow \neg \alpha)$ contra position

$\Large (\alpha \Rightarrow \beta) \equiv (\neg \alpha \lor \beta)$ Implication elimination

$\Large (\alpha \Leftrightarrow \beta) \equiv ((\alpha \Rightarrow \beta) \land (\beta \Rightarrow \alpha))$ Biconditional Elimination

$\Large\neg(\alpha \land \beta) \equiv (\neg \alpha \lor \neg \beta)$ De Morgan

$\Large \neg(\alpha \lor \beta) \equiv (\neg \alpha \land \neg \beta)$ De Morgan

$\Large (\alpha \land (\beta \lor \gamma)) \equiv ((\alpha \land \beta) \lor (\alpha \land \gamma))$ distribution of $\Large \land$ over $\Large \lor$

$\Large (\alpha \lor (\beta \land \gamma)) \equiv ((\alpha \lor \beta) \land (\alpha \lor \gamma))$ distribution of $\Large \lor$ over $\Large \land$

## Proof by Resolution
Motivation:
* Need a complete
* Resolution + Search = completeness
Resolution rule:
* Combines clauses with completeness literals
* Produces a resolvent
Soundness:
* Resolution preserves truth

## Conjunctive Normal Form (CNF)
Definition:
* Conjunction of clauses
* Each clause is a disjunction of literals
Conversion stops:
1. Eliminate $\Large \iff$
2. Eliminate $\Large \implies$
3. Push $\Large \neg$ inwards (De Morgan)
4. Distribute $\Large \land$ or $\Large \lor$
Convert CNF to a sentence.

## Resolution Algorithm
* Proof by Contradiction
* To show $\Large KB \models \alpha$:
	1. Form $\Large KB \land \alpha$
	2. Convert to CNF
	3. Apply Resolution
	4. Empty Clause $\Large \implies$ Entailment proven
* Outcomes
	* Empty clauses found  -> $\Large KB \models \alpha$ 
	* No new clauses -> $\Large KB \not\models \alpha$ 


## Horn Clauses
Some simple forms of sentences do not require proof by resolution. We introduce Horn clauses for which very efficient inference algorithms exist.

### Horn Clause
* propositional symbols; or
* (conjuntion of symbols) $\Large \implies$ symbol

Which are Horn clauses?
* $\Large (L_{1,1} \land Breeze ) \implies B_{1,1}$ Yes
* $\Large L_{1,1} \qquad (\equiv true \implies L_{1,1}$ Yes
* $\Large (L_{1,1} \lor Breeze) \implies B_{1,1}$ No

A knowledge base consisting of Horn clauses only requires Modus Ponens as an inference method:

$$\Large
\frac{\alpha_1 , \space ... , \space \alpha_n \qquad \alpha \land \space ... \space \land \alpha _n \implies \beta}{\Large \beta}
$$

## Forwards Chaining & Backwards Chaining
### Forwards Chaining
* Data driven
* Automatically derives all consequences
* Linear time
* May do unnecessary work

### Backward Chaining
* Goal-driven
* Starts from query
* Linear time
* Often more efficient for problem solving

### Both are
* Sound
* Complete
#### Summary
* Knowledge-Based Agent = KB + inference engine
* Syntax vs. Semantics vs. models are distinct
* Entailment defined via sets of models
* Propositional Logic has finite models
* Enumeration is correct but exponential
* Resolution is sound and complete 
* CNF is required for resolution
* Horn clauses allow efficient chaining