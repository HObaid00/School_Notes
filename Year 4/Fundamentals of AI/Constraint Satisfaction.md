In this note we will discuss the Constraint Satisfaction Problem Model
### What is Constraint Satisfaction Problem?
#### Definition:
* A CSP is a tuple $(X, D, C)$
* $X =$ {${x_1, x_2, ... , x_n }$} variables
* $D =$ {$d_1, d_2, ... , d_n$} domain values
* $C =$ {$c_1, c_2, ... , c_n$} constraints
Each constraint is a pair (scope, relation) defining allowed combinations
#### Key Difference from standard search:
* Standard search: states are atomic
* Constraint Satisfaction Problems: states are factored into variables
* Goal: Assign all variables such that all constraints are satisfied

### Why Constraint Satisfaction Problems matters:
* Exploits problem structure
* Enables powerful general-purpose algorithms
## Constraint Graph
* Nodes $=$ Variables
* Edges $=$ Constraint between variables
* Independent sub-graphs -> independent sub-problems
* Fixing one variable reduces neighbors domains
Important consequences: Structure dramatically reduces search complexity
## Types of Constraints
* Unary: One variable
* Binary: Two Variables
* High Order: Reducible to binary
* Soft Constraints

## Backtracking Search

#### Core Idea:
* [[Depths-First Search]]
* Assign one variable at a time
* Assignments are commutative
* Stop when assignment is complete
#### Complexity:
* Worst case $O(d^n)$
* Much Better in practice with heuristics + inference
#### Backtracking Algorithm (must understand flow)
1. If assignment complete -> return solution
2. Select unassigned variable
3. Try values in order
4. Check consistency
5. Apply inference
6. Re curse or backtrack

## Variable Selection Heuristics 
### Minimum Remaining Values (MRV)
* Choose variable with legal values
* Fail-first principle
* Strong pruning effect
### Degree Heuristic
* Choose variable involved in most constraints
* Under when MRV ties or early in search
**Exam Note**: Variable Selection = *fail early*

## Variable Selection Heuristic
Least Constraining Value (LCV):
* Choose value that eliminating **fewest options** for neighbors
* Increase chance of finding a solution quickly
**Exam Note:** Value Selection = *fail state*
## Inference in CSPs
* Logic deduction to reduce domains
* Applied:
	* After each assignments
	* or as preprocessing
## Forward Checking 
* After $X_i$ , remove inconsistent values from neighbors $X_j$
* Only affects **immediate neighbor**
* Defect failure early

Limitation:
* Does not propagate further constraints

## Arc Consistency
Definition:  Variable $X_i$ is arc-consistency $X_j$ if :
* For every value in $D_i$ , there exists some value in $D_j$ satisfying the constraint.
Arc Consistency id directional

## AC-3 Algorithm
Purpose:
* Enforces arc consistency throughout the CPS
Key Steps:
1. Initialize queue of arcs
2. Remove inconsistent values
3. If a domain becomes empty -> failure
4. Re-add affected arcs
* Time Complexity: $O(c*d^3)$
Used:
* As preproccessing
* Or after each assignment

## Structure of CSPs
Independent sub problems:
* separate connected components
* solve independently
* Exponential -> linear improvement

## Tree Structure CSPs
* Constraint graph is a tree
* Solvable in $O(n*d³)$ time
* Step:
	1. Choose root and order variables
	2. Enforce directed arc consistency
	3. Assign values top-down without backtracking

## Nearly Tree Structured CSPs
Conditioning:
* Instantiate a small set of variable
* Remaining problem becomes a tree
* Runtime: $O(d^c * (n - c)* d^2)$
* Conceptual understanding only
Tree Decomposition
* Break problem into overlapping sub problems
* Solve sub problems independently
* Combine solution consistently 
* Conceptual understanding only

## Summary
* CSP = variables + domains + constraints
* Backtracking is the base algorithm
* MRV & Degree -> Variable choice
* LCV -> Value choice
* Forward checking < Arc consistency
* Structure of constraint graph dominates complexity
* Tree-structured CSPs are tractable

