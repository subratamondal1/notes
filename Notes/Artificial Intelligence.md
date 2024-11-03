[[02-11-2024]] #piyush

# Artificial Intelligence
![[Pasted image 20241102231223.png]]
## Key Terminologies
- **Search:** means finding something. In AI it is about finding a solution to a problem.
- **Agent:** is an Entity that can perceive its Environment and can Act upon it.
	- E.g: In a Navigator App
		- **Entity:** Self-Driving Car 
		- **Environment:** GPS, Maps, Realtime Traffic Data.
		- **Act:** Move left, right, speedup, slow down.
	- E.g: **Entity** -  Computer Systems, Softwares.
- **State:** Configurations of an Agent in its environment.
- **Initial State:** Starting point of the Search Algorithm.
- **Final State:** End point (Goal) of the Search Algorithm.
- **Goal State:** condition that determines whether a given state is a goal state or not.
- **Action:** Choices that can be made in a state.
- **Transition Model:** Describes how an **action** changes the **state** of a system.  Represented as a function: $\text{Result}(s, a)$.
     - $( s )$ represents the **current state**.
     - $( a )$ represents the **action** applied to that state.
	 ![[Pasted image 20241102185426.png]]
* **State Space:** is nothing but Sample Space that is all the possible outcomes in an experiment.
	* Represented as a Directed Graph where states are represented by Nodes and Actions are represented by Edges with Arrows.
	  ![[Pasted image 20241102190134.png]]
	* **Path Cost:** A numerical cost associated with a given path. Calculated via the weighted edges in a graph.
	  ![[Pasted image 20241102190617.png]]
* **Solution:** A sequence of actions that take us from the initial state to the goal state.
* **Optimal Solution:** A solution that has the Lowest Path Cost among all the solutions.

### Components of Search Algorithms
- Initial State
- Actions
- Transition Model
- Goal Test
- Path Cost Function
- Solution, Optimal Solution

![[Pasted image 20241102225913.png]]

### Approach to solve a search problem
![[Pasted image 20241102230134.png]]

![[Pasted image 20241102230812.png]]

## Uninformed/Blind Search Algorithms
- Uninformed Search Algorithms are used to solve problems where the **solution is not known in advance**. E.g:
	- **BFS (Breadth First Search) - Queue (FIFO)**
	- **DFS (Depth First Search) - Stack (LIFO)**
	- **UFS (Uniform Cost Search)**
	- **DLS (Depth Limited Search)**
	- **Iterative Deepening DFS (IDDFS)**
- **Completeness:** A search algorithm is complete if it guarantees to find a solution if it exists.
- **Optimality:** An optimal search algorithm finds the shortes t path to the goal.
### When to use Uninformed Search Algorithms
- Efficient for Small to Moderate Sized Search Spaces.
* Where domain-specific knowledge is unavailable/limited.
* Good for simple and general purpose approach to solve problems.
### Limitations of Uninformed Search Algorithms
- Inefficient for Large Sized Search Spaces.
- Might lead to unnecessary exploration of search spaces as they do not has any domain-specific knowledge.

### DFS vs BFS

#### Depth-First Search (DFS) - Stack
- Explores one branch of possibilities as deeply as possible before backtracking
- Particularly useful for exhaustive search in decision trees and state spaces
- Primary application: Game playing AI, where evaluating move sequences deeply is important
- Strategy: Goes deep before going wide

#### Breadth-First Search (BFS) - Queue
- Explores all possibilities at the current level before moving to the next level
- Optimal for finding shortest paths or minimal solutions
- Primary application: Pathfinding algorithms, GPS navigation, robotics
- Strategy: Goes wide before going deep

#### Comparison Based on Key Criteria

##### 1. Completeness
- **DFS**: Complete in finite state spaces, but may not terminate in infinite spaces
- **BFS**: Complete in both finite and infinite state spaces (with finite branching)
- Key Difference: BFS guarantees finding a solution if one exists, while DFS might get stuck in infinite paths

##### 2. Time Complexity
Given:
- b = branching factor
- d = depth of solution/goal

Performance characteristics:
- **DFS**: $O(b^d)$
  - Efficient when solutions are deep
  - Can get trapped exploring deep paths that don't lead to solutions
  
- **BFS**: $O(b^d)$
  - Efficient when solutions are shallow
  - Must explore exponentially growing levels
  
Situational Performance:
- Deep solutions: DFS performs better
- Shallow solutions: BFS performs better

##### 3. Space Complexity
Given the same parameters:
- **DFS**: O(bd) - Linear space complexity
  - Only needs to store the current path
  - More memory efficient
  
- **BFS**: $O(b^d)$ - Exponential space complexity
  - Must store all nodes at current level
  - Requires significantly more memory

#### 4. Quality of Solutions

**DFS**:
- First solution found may not be optimal
- Better for:
  - Deep tree exploration
  - Game tree analysis
  - Problems requiring exhaustive search

**BFS**:
- Guarantees shortest path solution
- Better for:
  - Finding optimal paths
  - Minimal solutions
  - Navigation problems

#### Finite vs Infinite Search Spaces

1. Finite Search Spaces:
   - Both algorithms are complete
   - Both will systematically explore entire space
   - Termination guaranteed for both

2. Infinite Search Spaces:
   - DFS may not terminate if it goes down an infinite path
   - BFS will find a solution if one exists (with finite branching)
   - Neither will terminate if no solution exists

#### Practical Implementation Considerations

1. Memory Management:
   - DFS is preferred when memory is limited
   - BFS requires substantial memory for large branching factors

2. Solution Quality Requirements:
   - Use BFS when optimal paths are required
   - Use DFS when any valid solution is acceptable

3. Problem Structure:
   - Use DFS for deep, tree-like structures
   - Use BFS for shallow, graph-like structures
#### Q1.Gate Pyq
![[Pasted image 20241103234233.png]]
The question asks about the behavior of BFS and DFS in reaching a goal state numbered 6, with specific conditions on the successor function and state expansion order. Here’s how we approach it:

1. **Initial State and Successors**:
   - The start state is 1.
   - For a state numbered \( n \), its successors are \( n+1 \) and \( n+2 \).

2. **Search Strategy for BFS and DFS**:
   - **BFS** (Breadth-First Search): Expands nodes level by level. Starting from 1, it will expand in ascending order, leading to states: 2, 3, 4, 5, 6, etc.
   - **DFS** (Depth-First Search): Goes as deep as possible along each branch before backtracking. Given the successor function, DFS will explore 1, then 2 (following \( n+1 \) path), then 3, 4, 5, 6, etc., potentially reaching state 6 without expanding extra nodes beyond what BFS does at this level.

3. **State Expansions**:
   - Since both BFS and DFS are expanding in ascending order and both will encounter state 6 within similar initial expansions, they should reach the goal state 6 after expanding the same number of states.

4. **Conclusion**:
   - Both BFS and DFS will expand an equal number of states to reach the goal state number 6.

##### Answer:
The correct choice is:
**(C) Both BFS and DFS expand an equal number of states.**
## Informed Search Algorithms
- They uses heuristic or domain-specific knowledge in the searching process. They also prioritize exploring paths that are more likely to lead to a solution, making them more efficient. E.g:
	- **Greedy Best-First Search.**
	- **A* Search**
### When to use Informed Search Algorithms
- Efficient for Complex and Large Sized Search Spaces.
- Where heuristic or domain-specific knowledge can be used.
### Limitations of Informed Search Algorithms
- Performance depends on the quality of the heuristic or domain specific knowledge.
## Adversarial Search
- Deals with decision making in competitive environments. Widely used in games and competitive scenarios where an AI Agent can make an optimal move (action) based on the opponent's move (action). E.g:
	- **Minimax**
	- **Depth Limited Minimax**
	- **Alpha-Beta Pruning**


