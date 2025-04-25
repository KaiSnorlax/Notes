1950's (First wave AI)
* Core Focus: Mimic human decisions through rule-based systems

If you want to find the coit tower, you will look for the tower. If you are an AI you may use BFS to find the tower.

Search problem solver
* Humans solve problems by having a goal in mind
*
Cognitive Psycology meets  AI
* People estimate how far they are from the goal
* People avoid paths that look wrong and dont search blindly
* This is called Heuristic

Heuristic Functions
* a function h(n) that estimates teh cost frm a given state n to the goal in the search problem.
* Guides the search by predicting which paths are likely cheaper or faster to the solution

Common Heuristic Functions
Grid Navigation
* Euclidean distance
* Manhattan distance

8-tile
* Misplaced tile count
* Manhattan distance to goal positions

Traveling Salesman Problem
* Minimum spanning tree over unvisited cities

Robot motion planning
* Straight-line distance to the target, ignoring obstacles

Planning problems
* Number of unmet preconditions for the goal

Making Heuristic Functions
Use relaxed problems
- Make the problem easier

Use domain knowledge
- Encode expert insight into distance, effort, or utility

Use learned heuristics
- Train a model to approx. cost-to-go


GBFS
- A heuristic-driven search algorithm that explores nodes based on their estimated cost to the goal, using a heuristic function h(n).
- This prioritizes the most promising node at each step, aiming to reach the goal quickly
- How it works
	- Selects the node with the lowest h(n) value from the open list
	- Expands that node, evaluates its neighbors, and repeats until the goal is found or no nodes remain.
	- $expand(n)|n$
	- Ignores path cost g(n) making it greedy but faster


A*
- Is optimal if heuristic function h(n) is admissable

Variations of A*
Weighted A*
Objective: Accelerate A* by favoring nodes the look closer to the goal
modified exaluations function:
$f(n)=g(n)+w*h(n)$, with $w>1$

Tradeoff between time and functionality
* Good enough and time sensitive