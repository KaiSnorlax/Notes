Before human like intelligence was mimicked with
-> Classical search
	-> Trial and Error
-> Adversarial search
	-> Game rules
	-> Probability from experience

Now we will look at logic
-> Conclusions from facts


How does Akinator work?
has a huge database with facts
- Asks yes/no questions to narrow down
- Updates guesses based on user answers
- Tries to infer waht you're thinking using prev. 

We will see how logic based agent work and what they do
How to represent knowledge
How to reason and infer
How to structure knowledge

What is a knowledge-based agent
- has its "knowledge"
- Precepts (can update the knowledge base)
	- can query the knowledge base to find some truth to move us twoards the goal
- Execute and Repeat

This agent has the ability to learn new facts about the world
Adapt to new situations
move beyond hard-coded behavior
support flexible problem solving
enable incremental learning and updating


Wumpus world environment
Performance Measure
- +1000 for climbing out with the gold
- -1000 for falling into a pit or being eaten by the Wumpus
- -10 for firing the arrows
- -1 for each action taken

Environment:
- 4x4 grid of rooms, surrounded by walls
- Agent starts at [1,1], facing east
- Gold and Wumpus randomly placed (excluding [1,1])
- Each square (except [1,1]) has a 20% chance of containing a pit

Actuators:
- Move forward, Turn left, Turn right
- Grab (pick up gold)
- Shoot (fire one arrow in facing direction)
- Climb (exit cave, only from [1,1])


Representing knowledge formally
	reasoning is interleaved with exploration: act -> sense -> update -> plan


English:
"The Wumpus might be nearby."

Logic:
$S_{1},2\$


Propositional Logic: Syntax I
- atomic propositions represent basic, indivisible facts about the world.
#### Example:
P1,2: "There is a pit in (1,2)"

Propositional Logic: Syntax II
Logical connectives


Models and Semantic
- Writing a logical sentence does not guarantee it is true.


Semantic: Meaning
Models 

| P_11 | False |
| ---- | ----- |
| B_12 |       |
| G_23 |       |

What is a knowledge base?
- The set of true facts for the world it is in

Model checking
- which models your KB is true in
- Single model, check if everything in KB is true for this model
- Many models, check if every permutation is correct

-> can check with a truth table
- The number of rows grow exponentially with the number of atomic propositions.

## Definition : Validity
## Definition : Satisfiability

## Definition : Un


How to agents draw conclusions?

iference
- based on info in KB, and precepts, i can find somehting that 

Soundness

Completeness

Ideal Inference System:


Proof Methods:
- We do this to get  systematic procedures for deriving conclusions from a knowledge base.

Can use two approaches:
- truth tables
- deduction


Inference Rule:
If a is true, and a implies B is true, then we can infer that B is true

Limitations of propositional logic:

- no internal structure to propositions
- Cannot represent general statements compactly
	- cant do Cats -> Cute would have to
	- Cat1 -> Cute
	- Cat2 -> Cute
- no quantification over objects
- Rigid and non-scalable
- Lacks expressiveness needed for real-world knowledge

#### Example : 20 Questions bot 
Knowledge Base (KB):
