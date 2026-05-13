## What is Search in AI?
* Search = finding a sequence of action that leads from an initial state to a goal state
* Used when:
	* The environment is discrete
	* The agent must plan ahead, not react greedily
* Search operates on abstract models, not raw sensor data

## Formulating a Well-Defined Search Problem
A search problem is formally defined by six components:
1. State of space: Set of all possible states.
2. Initial State: Starting point of the agent.
3. Action: Actions applicable in each state
4. Transition model: Result (s, a) -> Next State
5. Goal test: Checks whether a state is a goal
6. Action cost: Cost of transitioning between states

## Search Trees and Frontiers
* Root: Initialize State
* Nodes: States reached
* Edge: Action
* Leaves: Unexpected Nodes
* Frontier: Unexplored Leaves

Search proceeds by:
1. Selecting a node from the frontier
2. Expanding it
3. Adding successors to the frontier

## Tree Search
* Does not remember visited states
* May:
	* Loop Forever
	* Expanded identical states repeatedly
* Simpler but not efficient

## Graph
* Maintain a reached (visited) set
* Expands a state only once (or only if cheaper-path is found)
* Prevents cycles
Graph Search is safer but not always necessary

## Performance Measures for Search Algorithms
1. Completeness: Will if find a solution if one exists?
2. Optimally: Does it find the lowest-cost solution?
3. Time complexity: Number of nodes expanded
4. Space Complexity: Maximum memory usage

## Uninformed Search
* No extra knowledge beyond:
	* States
	* Actions
	* Goal tests
	* Costs
* Cannot estimate distance to the goal
### Breadth-First-Search
#BFS 
Idea
* Expanded shallowest nodes first 
* Uses a First In First Out (FIFO) queue
Properties
- [v] Complete (finite branching factor)
- [v]  Optimal    [ x ] (only if step costs are equal)
* Time Complexity $O(b^d)$
* Space Complexity $O(b^d)$
Key drawbacks:
* Exponential memory consumption -> quickly infeasible

### Uniform-Cost Search  (UCS/Dijkstra)
#Uniform
Idea:
* Expanded node with lowest path cost $g(n)$
* Frontier is a priority queue ordered by $g(n)$
Properties:
- [v] Complete [ x ] (positive step costs)
- [v] Optimal    [ x ] (for arbitrary costs)
* BFS is a Special case of UCS when all costs are equal
Key Insight:
* UCS expands cheapest paths first, not shallowest paths.

### Depths-First Search
#DFS
Idea:
* Expand deepest node first
* Uses a Last In First Out (LIFO)
Properties:
* Complete [   ] (can get stuck in infinite depth)
* Optimal    [   ] 
* Time Complexity $O(b^m)$
* Space Complexity $O(b*m)$
Advantage: **Very low memory usage**

### Depth-Limited Search 
#DLS
* DFS with a maximum depth limit
* Avoid infinite descent
* Still not optimal
* Completeness depends on correct depth limit

### Iterative Deepening Search
#IDS
Idea:
* Repeatedly apply depth-limited DFS
* Increase depth Unit step by step
Properties:
- [v] Complete 
- [v] Optimal (equal step by step)
* Time Complexity $O(b^d)$
* Space Complexity $O(b*d)$
**Combines BFS optimal with DFS memory efficiency**
### Bidirectional Search
* Search forward from start **and backwards**
* Steps when frontiers meet steps from goal 
* Reduces complexity $O(b^d)$ -> $O(b^{d/2})$
* Requires:
	* Reversible actions
	* Explicit goal state
### Summary
* Search problems require formal definition
* Search trees grow exponentially
* **Graph search prevents cycles**
* BFS = shallowest first
* Best-First Search generalizes all
* DFS trades completeness for memory
* Iterative deepening is often the best uninformed strategy

## Informed Search
* Uses Heuristics
* Knows when states are promising

### Heuristic Function (n)
* Definition: $h(n)$ estimates the cost of the cheapest path from node $n$ to a goal 
* Constraints:
	* $h(n)$ $\geqslant$ $0$
	* $h(\hat{n})$ $=$ $0$ for goal node $\hat{n}$
* Heuristics are problem-specific
* Heuristic guide search but do not replace path costs

### Best-First Search Framework
* Informed search strategies are best-first search with $f(n)= evaluation$
* The node with lowest $f(n)$ is expanded next
* Different informed searches differ only in $f(n)$

### A* Search
#Astar 
Core Idea:
* Combines 
	* Actual path cost so far $g(n)$
	* Estimated remaining cost $h(n)$
* Evaluation function: $f(n)=g(n)+h(n)$
### Greedy Best-First Search
#GreedyBFS
Idea: Use only the heuristic $f(n) = h(n)$
* Expands the node, estimates closest to the goal.
Properties:
- [v] Completeness if graph search is used
- [ ] Optimally
* Time Complexity $O(b^m)$
* Space Complexity $O(b^m)$
Key Insight:
* Can find sub-optimal solutions
* Can loop infinitely without a reached set
* Very fast with good heuristic, unreliable otherwise

### Admissible Heuristics 
* Never overestimate true costs $h(n) \leq h(n*)$*
* Guarantees:
	- [v] Completeness (positive costs)
	- [v] Optimally
- A* with admissible heuristics:
	- Never expands nodes with $f(n) > C$
	- Pranes entire subtrees automatically

### Consistent (Monotonic) Heuristic
* Stronger than admissibility: $h(n) \leq c(n, a, n') + h(n')$
* Equivalent to triangle inequality
* Guarantees:
	* Each node expanded at most once
	* No need to reinsert nodes into the frontier
* Ever consistent heuristic is admissible

### Admissible Vs Consistency
| Property                              | Admissible | Consistent |
| ------------------------------------- | ---------- | ---------- |
| Guarantees Optimal goal               | Yes        | Yes        |
| Guarantees optimal path to every node | No         | Yes        |
| Node re-expansion possible            | Yes        | No         |

### Performance of A*
- [v] Completeness (positive step costs)
- [v] Optimally (admissible heuristic)
- Time Complexity: $O(b^{\epsilon * d})$, $\epsilon = (h* - h) h*$
- Space Complexity  $=$ Time Complexity
A* performance depends critically on heuristic quality

### Limitations of A*
* High memory consumption
* Becomes infeasible for large problems
Memory-bounded variants:
* Iterative-Deepening A*
* Recursive Best-First Search (RBFS)
* Memory-Bounded A* (SMA*)

### Designing Heuristics
#### 1 Relaxed Problems
* Remove constraints from the original problem
* Optimal cost of relaxed problem $\leq$ original problem

#### 2 Patterns Databases
* Pre-compute optimal costs for sub-problems
* Store in a lookup table
* Combine heuristics safely
* Very powerful but memory-insensitive

#### 3 Heuristic Domination
* Heuristic $h_2$ dominates $h_1$ if: $h_2(n) \geq h_1(n)$ $\forall n$
* Dominating heuristics
	* Expanded fewer or equal nodes
	* Always preferable

## Admissible Heuristic
Since a heuristic is admissible if it doesn't overestimate the path it will take to get to the goal, in the context of two given heuristics $h_1(n)$, and $h_2(n)$  a dominating admissible heuristic will be:
$$\Large
h^\ast(n) = \max\{h_1(n), h_2(n)\}
$$ 
### Effective Branching Factors b*
* Measures heuristic quality empirically.
* Defined by: $N+1 = 1 + b* + (b*)^2 + ... + (b*)^d$
* Lower $b*$ -> better heuristic
* Allows comparisons across problems of different sizes.

### Summary
* Informed search uses heuristics $h(n)$
* Greedy best-first search is fast but not optimal
* A* is complete and optimal with admissible heuristics
* Consistent heuristics prevent re-expansion
* Better heuristics reduce effective branching factor
* Heuristics come from:
	* Relaxed Problems
	* Pattern databases



