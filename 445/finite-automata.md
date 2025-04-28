# Finite Automata
A model used for computers with *extremely* limited memory.

**Example**:
Imagine we have an automatic door. Whether or not the door should be open or closed is controlled by two pressure plates in front of and behind the door.

```tikz
\usetikzlibrary{automata, arrows.meta, positioning, calc, fit, chains, shapes}
\tikzset{
  ->,
  initial text=,
  shorten >=1pt,
  >={Stealth[round]},
  on grid,
  auto,
  node distance=2cm,
  bend angle=15,
}

\begin{document}
    \begin{tikzpicture}[
        % Define a style called "pad".
        pad/.style={rectangle,draw,align=center,minimum size=1cm}
      ]

      % Create nodes with the "pad" style.
      \node[pad] (f) {front\\pad};
      \node[pad] (r) [right=of f] {rear\\pad};

      % Draw a line starting 1 unit below the center of the pads going up two
      % units.  Tikz syntax is a little weird and takes some getting used to
      % for complicated things.
      \draw[-] ($(f)!0.5!(r) + (0,-1)$) node[below] {door} -- ++(0, 2);
    \end{tikzpicture}
\end{document}
```

The controller for the door is either in the open or closed state. As pressure is added to the pads, the controller will transition between those two states.

There are four different input conditions:
1. The front pad has pressure
2. The rear pad has pressure
3. Both pads have pressure
4. Neither pad has pressure

The way the controller will transition from open to closed can be represented as a follows:
```tikz
\usetikzlibrary{automata, arrows.meta, positioning, calc, fit, chains, shapes}
\tikzset{
  ->,
  initial text=,
  shorten >=1pt,
  >={Stealth[round]},
  on grid,
  auto,
  node distance=2cm,
  bend angle=15,
}

\begin{document}

\begin{tikzpicture}[
        % Every node will have its text center aligned.  This is only relevant
        % if the text is multiple lines.
        every node/.append style={align=center},
        % Make every state a little larger than normal.
        every state/.append style={minimum size=1.2cm},
      ]

      % Create states (the circles).
      \node[state] (c) {closed};
      \node[state] (o) [right=3 of c] {open};

      % Draw the lines between the nodes.  Let me know if you have any
      % questions!
      \draw (c) edge[bend left] node {front} (o)
                edge[loop above] node {rear\\both\\neither} ()
            (o) edge[bend left] node {neither} (c)
                edge[loop above] node {front\\rear\\both} ();
    \end{tikzpicture}

\end{document}
```

This information can also be described in a table:

|        | neither | front | rear   | both   |
| ------ | ------- | ----- | ------ | ------ |
| closed | closed  | open  | closed | closed |
| open   | closed  | open  | open   | open   |
___________________________________________

**Example**: automaton

```tikz
\usetikzlibrary{automata, arrows.meta, positioning, calc, fit, chains, shapes}
\tikzset{
  ->,
  initial text=,
  shorten >=1pt,
  >={Stealth[round]},
  on grid,
  auto,
  node distance=2cm,
  bend angle=15,
}

\begin{document}
    \begin{tikzpicture}
      % The initial state has an arrow coming in from the left.
      \node[state, initial] (1) {$q_1$};
      % An accepting state has a double circle.
      \node[state, accepting] (2) [right=of 1] {$q_2$};
      \node[state] (3) [right=of 2] {$q_3$};

      \draw (1) edge[loop above] node {$0$} ()
                edge node {$1$} (2)
            (2) edge[bend left] node {$0$} (3)
                edge[loop above] node {$1$} ()
            (3) edge[bend left] node {$0, 1$} (2);
    \end{tikzpicture}
\end{document}
```
This is the ==state diagram== of $M_1$.
- $q_1$,$q_2$, and $q_3$ are the states.
- $q_1$ is the start state.
- $q_2$ is an accept state.
- The arrows are transitions.

When the machine receives input strings (ex. 1011), it will process it and produce an output. This output is either accept, or reject. 

Processing begins in the start state. The machine receives the symbols from the input string one by one, left to right. After each symbol, the machine will transition from one state to another one. When the last symbol is read, the machine will produce an output of accept if the machine is in an accept state, if it is anywhere other than an accept state it will reject.

If $M_1$ receives an input of `1011`:
1. Start in $q_1$.
2. Read `1`, transition from $q_1$ to $q_2$.
3. Read `0`, transition from $q_2$ to $q_3$.
4. Read `1`, transition from $q_3$ to $q_2$.
5. Read `1`, transition from $q_2$ to $q_2$.
6. Accept because the machine is in an accept state at the end of the input.

This machine will accept any string containing at least one 1, and ending with an even number of 0s following the last 1.
___________________________________
## Definition
A finite automaton is a 5-tuple ($Q,\Sigma,\delta,q_0,F$), where
- $Q$ is a finite set called the *states*,
- $\Sigma$ is a finite set called that *alphabet*,
- $\delta: Q \times \Sigma \rightarrow Q$ is the *transition function*,
- $q_0 \in Q$ is the *start state*, and
- $F \subseteq Q$ is the *set of accept states* (these are sometimes called *final states*)

The machine $M_1$ can be described as:
$M_1=(Q,\Sigma,\delta,q_1,F)$ where:
- $Q=\{q_1,q_2,q_3\}$
- $\Sigma = \{0,1\}$
- $\delta$ is described by:

|       | 0     | 1     |
| ----- | ----- | ----- |
| $q_1$ | $q_1$ | $q_2$ |
| $q_2$ | $q_3$ | $q_2$ |
| $q_3$ | $q_2$ | $q_2$ |

- $F=\{q_2\}$

Where the above table is shorthand for $\delta(q_1,0)=q_1, \delta(q_1,1)=q_2,\dots$ 

## Definition
If $A$ is the set of all strings that machine $M$ accepts, we say that $A$ is the *language of machine $M$* and write $L(M) = A$. We say that $M$ *recognizes* $A$.

A machine may accept many strings, but it **always** recognizes exactly one language. If the machine accepts no strings, it still recognizes the empty language $\emptyset$.

---
### More examples of finite Automata
#### Ex1.)

```tikz
\usetikzlibrary{automata, arrows.meta, positioning, calc, fit, chains, shapes}

\tikzset{
  ->,
  initial text=,
  shorten >=1pt,
  >={Stealth[round]},
  on grid,
  auto,
  node distance=2cm,
  bend angle=15,
}

\begin{document}
    \begin{tikzpicture}
    \node at (-1.5,1.5) {$M_1$};
      \node[state, initial] (1) {$q_1$};

      \draw (1) edge[loop above] node {$0$} ()
                edge[loop right] node {$1$} ();
    \end{tikzpicture}
    \begin{tikzpicture}
    \node at (-1.5,1.5) {$M_2$};
      \node[state, accepting, initial] (1) {$q_1$};

      \draw (1) edge[loop above] node {$0$} ()
                edge[loop right] node {$1$} ();
    \end{tikzpicture}
\end{document}
```

$$
\begin{align}
M_1&=(\{q_1\},\{0,1\},\delta,q_1,\emptyset) \\
M_2&=(\{q_1\},\{0,1\},\delta,q_1,\{q_1\})
\end{align}
$$

where $\delta$ is given by:
$$
\begin{align}
	\delta:\ &Q \times \Sigma \rightarrow Q &&\\
	&(q_1,0) \mapsto q_1 &&\\
	&(q_1,1) \mapsto q_1 &&
\end{align}
$$

What is the language of $M_1$ and $M_2$?
$$
\begin{align}
L(M_1) &= \emptyset \\
L(M_2) &= \{w|w\ \text{is a string of 0's and 1's}\}
\end{align}
$$
#### Ex2.)

```tikz
\usetikzlibrary{automata, arrows.meta, positioning, calc, fit, chains, shapes}

\tikzset{
  ->,
  initial text=,
  shorten >=1pt,
  >={Stealth[round]},
  on grid,
  auto,
  node distance=2cm,
  bend angle=15,
}

\begin{document}
    \begin{tikzpicture}
    \node at (-1.5,1.5) {$M_3$};
      \node[state, initial] (1) {$q_1$};
      \node[state, accepting] (2) [right=of 1] {$q_2$};

      \draw (1) edge[loop above] node {$0$} ()
                edge[bend left] node {$1$} (2)
            (2) edge[loop above] node {$1$} ()
		        edge[bend left] node {$0$} (1);
    \end{tikzpicture}
    
    \begin{tikzpicture}
    \node at (-1.5,1.5) {$M_4$};
      \node[state, initial, accepting] (1) {$q_1$};
      \node[state] (2) [right=of 1] {$q_2$};

      \draw (1) edge[loop above] node {$0$} ()
                edge[bend left] node {$1$} (2)
            (2) edge[loop above] node {$1$} ()
		        edge[bend left] node {$0$} (1);
    \end{tikzpicture}

\end{document}
```
$$
\begin{align}
M_3&=(\{q_1,q_2\},\{0,1\},\delta,q_1,\{q_2\}) \\
M_4&=(\{q_1,q_2\},\{0,1\},\delta,q_1,\{q_1\})
\end{align}
$$

where $\delta$ is given by:
$$
\begin{align}
	\delta:\ &Q \times \Sigma \rightarrow Q &&\\
	&(q_1,0) \mapsto q_1 &&\\
	&(q_1,1) \mapsto q_1 &&
\end{align}
$$

| $M_3$ | 0     | 1     | //  | $M_4$ | 0     | 1     |
| ----- | ----- | ----- | --- | ----- | ----- | ----- |
| $q_1$ | $q_1$ | $q_2$ | //  | $q_1$ | $q_1$ | $q_2$ |
| $q_2$ | $q_1$ | $q_2$ | //  | $q_2$ | $q_1$ | $q_2$ |

What is the language of $M_3$ and $M_2$?
$$
\begin{align}
L(M_3) &= \{w|w\ \text{is a string of 1's and 1's that end in a 1.}\} \\
L(M_4) &= \{w|w\ \text{is a string of 1's and 0's that ends in a 0 or is the empty string.}\}
\end{align}
$$

The empty string is denoted as $\epsilon$.

#### Ex3.)
![[Screenshot 2025-04-28 135221.png]]

$$
M_{5}=(\{q_0,q_1,q_2\},\{0,1,2,\texttt{<reset>}\},\delta,q_0,{q_0}) 
$$

where $\delta$ is given by:

| $M_5$ | $0$   | $1$   | $2$   | $\texttt{<reset>}$ |
| ----- | ----- | ----- | ----- | ------------------ |
| $q_0$ | $q_0$ | $q_1$ | $q_2$ | $q_0$              |
| $q_1$ | $q_1$ | $q_2$ | $q_0$ | $q_0$              |
| $q_2$ | $q_2$ | $q_0$ | $q_1$ | $q_0$              |

The language of $M_5$ is modulo 3.

## Definition
Let $M = \{Q,\Sigma,\delta,q_0,F\}$ be a finite automaton and let $w=w_1,w_2,\dots,w_n$ be a string where each $w_{i}\in \Sigma$. Then $M$ ==accepts== $w$ if a sequence of states $r_0,r_1,\dots,r_{i}\in Q$ exist where:
1. $r_0=q_0$
2. $\delta(r_i,w_{i+1})=r_{i+1}$ for all $i=0,1,\dots,n-1$ and
3. $r_{n}\in F$

## Definition
$L(M) = \{w\mid M$ accepts $w\}$
$M$ ==recognizes== $L(M)$.


## Definition
A language is called a ==regular language== if some finite automaton recognizes it.