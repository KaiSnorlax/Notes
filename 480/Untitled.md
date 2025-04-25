## Games
Human like Intelligence
* We are able to under stand rules
* Predict possible futures
* Anticipate opponents actions

How does a search algorithm decide what is "best"?

Games
- Two players
	- One turn at a time
- Zero-sum
	- One players gain is the others loss
- Ply (Turns)
- defined by

```
S_0: Initial state of the game
TO_MOVE(s): Which player moves in state s
ACTIONS(s): LEgal moves avaliable in state s
RESULT(s, a): The resulting state after action a is taken
IS_TERMINAL(s): Whether the game has ended
UTILITY(s, p): Final payoff for player p in terminal state s
```

Game Tree
- A tree structure where:
	- Nodes are the game states
	- Edges are legal moves
	- Leaves are terminal states (win/loss/draw)
	- Utility function is a function that assigns a numeric value to a terminal state, which indicates how good the outcome is for a player (+1: win, -1: loss, 0: draw)

Minimax tree
* A game tree where a numeric value is recursively assigned to each node, which represents the expected outcome for MAX, **assuming that both players play optimally**
* It alternates between:
	* MAX nodes: MAX chooses moves that maximizes the outcome (for MAX)
	* MIN nodes: MIN chooses moves that minimizes the outcome (for MIN)
	* The leaf nodes contain utility values
		* Values are propagated upwards to determine the best strategy
			* At MAX nodes, take maximum of child values
			* At MIN nodes, take minimum of child values
			* Tells MAX the best outcome they can guarantee no matter how MIN responds
	* These values represents how good/bad the outcome is for MAX
	* The path from root to the chosen action defines the optimal strategy

The Minimax search Algorithm
```python
def minimax(state, is_maximizing):
	if state.is_terminal():
		return state.utility()
	
	if is_maximizing:
		value = float('-inf')
		for action in state.get_actions():
			value = max(value, minimax(state.result(action), False))
			return value
	
	else:
		value = float('-inf')
		for action in state.get_actions():
			value = max(value, minimax(state.result(action), True))
			return value
```
* properties
	* Complete
	* Optimal
	* Time complexity O(b^m) where:
		* b is branching factor (# of legal moves)
		* m is depth of the tree
	* Space complexity
		* O(bm) if actions are generated at once
		* O(m) if actions are generated one at a time using recursion

Non-Zero Sum Games
- Utility values represent individual outcomes, not direct opposites
- Each node has a vector of utilities <vA, vB> for players A and B
- Terminal states return outcome vectors, not scalars
- No winner
- All players try to maximize their score