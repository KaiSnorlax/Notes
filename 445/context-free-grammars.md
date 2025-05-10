# Context Free Grammar

#### Example:
Let $G_1$ be the CFG:
$$
\begin{align}
A \rightarrow &\ 0A1\\
A \rightarrow &\ B\\
B \rightarrow &\ \#
\end{align}
$$
Here, A and B are variables, while # is a terminal.
Additionally, A is the start variable (*a terminal cannot be a variable, and there may only be ONE start variable*).

An example of a derivation of a string from the language:
$$
\begin{flalign*}
A &\Rightarrow 0A1 \\
  &\Rightarrow 00A11 \\
  &\Rightarrow 000A111 \\
  &\Rightarrow 000B111 \\
  &\Rightarrow 000\#111 \\

\end{flalign*}
$$
So, $000\#111 \in L(G_1)$

The language of $G_1$ is: $L(G_1)=\{0^{n}\#1^{n}\mid n \ge 0\}$

---
## Definition
A context free grammar is a 4-tuple $(V,\Sigma,R,S)$ where:
1. $V$ is a finite set called the variables,
2. $\Sigma$ is a finite set disjoint from $V$ called the terminals,
3. $R$ is a finite set of rules each rule being a variable and a string of variables and terminals,
4. $S \in V$ is the start variable.

From the example above, $G_{1}= (\{A,B\},\{0,1,\#\},\{A \rightarrow 0A1 ,A \rightarrow B, B \rightarrow \#\}, A)$

We can say that $A$ yields $0A1$, written as $A \Rightarrow 0A1$.
We can say that $A\xRightarrow{*}$

## Definition
If $u,v$ and $w$ are strings of variables and terminals, and $A\rightarrow w$ is a rule of the grammar, we say that $uAv$ yields $uwv$, written as $uAv \Rightarrow uwv$. We say that $u$ derives $v$, written as $u \xRightarrow{*} v$, if $u=v$ or if a sequence $u_1,u_2,\dots,u_k$ exists for $k \ge 0$ and $u \Rightarrow u_{1}\Rightarrow u_{2} \Rightarrow \dots \Rightarrow u_{k} \Rightarrow v$.

## Definition
The language of the grammar is the set $L(G)=\{w \in \Sigma^{*} \mid S \xRightarrow{*} w\}$.

---

#### Example:
Let $G_2$ be a CFG for mathematical expressions with the following substitution rules:
$$
\begin{align}
	\mathtt{<EXPR>} &\rightarrow \mathtt{<TERM>|<EXPR>+<TERM>|<EXPR-<TERM>} \\
	\mathtt{<TERM>} &\rightarrow \mathtt{<FACTOR> | <TERM * <FACTOR> | <TERM> / <FACTOR>} \\
	\mathtt{<FACTOR>} &\rightarrow \mathtt{<POWER> | -<FACTOR>} \\
	\mathtt{<POWER>} &\rightarrow \mathtt{<ATOM> | <ATOM> ** <FACTOR>} \\
	\mathtt{<ATOM>} &\rightarrow \mathtt{<LITERAL>|(<EXPR>)} \\
	\mathtt{<LITERAL>} &\rightarrow \mathtt{<DIGIT> | <DIGIT><LITERAL>} \\
	\mathtt{<DIGIT>} &\rightarrow \mathtt{0|1|2|3|4|5|6|7|8|9}

\end{align}
	
$$
Derivation for the string 123 (Parse Tree):

```tikz
\usetikzlibrary{trees}

\begin{document}

\begin{tikzpicture}[
  level distance=1.5cm,
  sibling distance=2.5cm,
  edge from parent/.style = {draw, -stealth}
]

\node {$<EXPR>$}
    child { node {$<TERM>$}
      child { node {$<FACTOR>$}
        child { node {$<POWER>$}
          child { node {$<ATOM>$}
            child { node {$<LITERAL>$}
              child { node {$<DIGIT>$} 
	              child { node {$1$}}}
              child { node {$<LITERAL>$} 
	              child { node {$<DIGIT$}
		              child {node {$2$}}}
	              child { node {$<LITERAL>$}
			              child { node {$<DIGIT$}
				              child { node {$3$}}}}}
            }
          }
        }
      }
    };

\end{tikzpicture}
\end{document}
```

---


#### Example:
Let $G_3$ be a CFG for arithmetic expressions with the following substitution rules:

$$
\begin{align}
	\mathtt{E} &\rightarrow \mathtt{E\ |\ E+T} \\
	\mathtt{T} &\rightarrow \mathtt{F\ |\ T*F} \\
	\mathtt{F} &\rightarrow \mathtt{a\ |\ (E)} \\
\end{align}	
$$
Derivation for the string $a+a*a$ (Parse Tree):
```tikz
\usetikzlibrary{trees}

\begin{document}

\begin{tikzpicture}[
  level distance=1.5cm,
  sibling distance=2.5cm,
  edge from parent/.style = {draw, -stealth}
]

\node {$E$}
    child { node {$E$}
	    child { node {$T$}
		    child { node {$F$}
			    child { node {$a$}}}}}
    child { node {$+$}}
    child { node {$T$}
	    child { node {$T$}
		    child { node {$F$}
			    child { node {$a$}}}}
	    child { node {$*$}}
		child { node {$F$}
			child { node {$a$}}}};
\end{tikzpicture}
\end{document}
```


---

#### Example:
Let $G_4$ be a CFG for arithmetic expressions with the following substitution rules:

$$
\begin{align}
	\mathtt{E} &\rightarrow \mathtt{E + E\ |\ E * T\ | \ (E)} \\
\end{align}	
$$

Parse tree 1 (interpreting as $(a+a) * a$):
```tikz
\usetikzlibrary{trees}

\begin{document}

\begin{tikzpicture}[
  level distance=1.5cm,
  sibling distance=2.5cm,
  edge from parent/.style = {draw, -stealth}
]

\node {$E$}
    child { node {$E$}
	    child { node {$E$}
		    child { node {$a$}}}
	    child { node {$+$}}
	    child { node {$E$}
		    child { node {$a$}}}}
    child { node {$*$}}
    child { node {$E$}
	    child { node {$a$}}};

\end{tikzpicture}
\end{document}
```

Parse tree 2 (interpreting as $a+ (a * a)$):
```tikz
\usetikzlibrary{trees}

\begin{document}

\begin{tikzpicture}[
  level distance=1.5cm,
  sibling distance=2.5cm,
  edge from parent/.style = {draw, -stealth}
]

\node {$E$}
    child { node {$E$}
	    child { node {$a$}}}
    child { node {$+$}}
    child { node {$T$}
	    child { node {$E$}
		    child { node {$a$}}}
	    child { node {$*$}}
	    child { node {$E$}
		    child { node {$a$}}}};

\end{tikzpicture}
\end{document}
```

**This grammar is ambiguous because the same string can have multiple parse trees. The standard order of operations is not enforced. This can be unambiguous by explicitly using parentheses in expressions or by structuring grammar rules to enforce operator precedence (as in previous example).**


---
## Definition 
Any language that can be generated by a context free grammar (CFG) is called a ==context free language== (CFL)

#### Example:
$\{O^n\#1^n|n\ge0\}$ is context free, but not regular

#### Example:
A CFG $G_1$ given by $\mathtt{S} \rightarrow \mathtt{aSb\ |\ SS\ |\ \epsilon}$
$$
\mathtt{S} \Rightarrow \mathtt{aSb} \Rightarrow \mathtt{ab}
$$
Therefore $ab \in L(G_1)$
We can describe the language of $G_1$ as being all properly nested pairs of a's and b's.

A similar language would be $\mathtt{S} \rightarrow \mathtt{(S)\ |\ [S]\ |\ \{S\}\ |\ SS\ |\ \epsilon}$ 

#### Example:
Construct a CFG to generate $\{0^n1^n|n\ge0\}\cup\{1^n0^n|n\ge0\}$
Dealing with unions is easy with CFG:

* Grammar for $\{0^n1^n|n\ge0\}$: $\mathtt{B} \rightarrow \mathtt{0B1\mid \epsilon}$
* Grammar for $\{1^n0^n|n\ge0\}$: $C \rightarrow 1C0 \mid \epsilon$

To combine them, we make a start variable to either $B$ or $C$:
$$
\begin{align}
	\mathtt{A} &\rightarrow \mathtt{B\mid C}\\
	\mathtt{B} &\rightarrow \mathtt{0B1\mid \epsilon}\\
	\mathtt{C} &\rightarrow \mathtt{1C0\mid \epsilon}
\end{align}
$$

---

## Definition
A CFG is in ==Chomsky normal form== if every rule is of the form $A \rightarrow BC$ or $A\rightarrow a$ where $a$ is any terminal and $A$,$B$, and $C$ are any variables - except that $A$, $B$ and $C$ may not be the start variable. In addition we permit the rule $S\rightarrow \epsilon$, where $S$ is the start variable.

- CFG makes it easy to count the number of substitutions to get to a certain string.

*Can only be a Variable -> 2 Variables, or Variable -> terminal or start variable -> $\epsilon$*

## THEOREM. Any CFL is generated by a CFG in Chomsky normal form.
*This is only the proof idea*

Proof Idea:
	1. Add a new start variable 
	2. Eliminate all $\epsilon$ rules
	3. Eliminate all "unit" rules if the form $\mathtt{A}\rightarrow\mathtt{B}$
	4. Convert all other rules


1. We add the new start variable $S$.
	$S \rightarrow A$
	$A \rightarrow B \mid C$
	$B \rightarrow 0B1 \mid \epsilon$
	$C \rightarrow 1C0 \mid \epsilon$
2. We eliminate all the $\epsilon$ rules.
	$S \rightarrow A$
	$A \rightarrow B \mid C \mid \epsilon$
	$B \rightarrow 0B1 \mid \epsilon$
	$C \rightarrow 1C0 \mid \epsilon$

	$S \rightarrow A$
	$A \rightarrow B \mid C \mid \epsilon$
	$B \rightarrow 0B1 \mid 01$
	$C \rightarrow 1C0 \mid \epsilon$

	$S \rightarrow A \mid \epsilon$
	$A \rightarrow B \mid C$
	$B \rightarrow 0B1 \mid 01$
	$C \rightarrow 1C0 \mid \epsilon$

	$S \rightarrow A \mid \epsilon$
	$A \rightarrow B \mid C$
	$B \rightarrow 0B1 \mid 01$
	$C \rightarrow 1C0 \mid 10$

3. Eliminate all "unit" rules if the form $A \rightarrow B$
	$S \rightarrow \colorbox{gray}{A} \mid \epsilon$
	$A \rightarrow \colorbox{teal}{B} \mid \colorbox{purple}{C}$
	$B \rightarrow 0B1 \mid 01$
	$C \rightarrow 1C0 \mid 10$

	$S \rightarrow \colorbox{gray}{0B1\ |\ 01\ | 1C0\ |\ 10} \mid \epsilon$
	$\colorbox{gray}{A} \rightarrow \colorbox{teal}{0B1\ |\ 01} \mid \colorbox{purple}{1C0\ |\ 10}$
	$\colorbox{teal}{B} \rightarrow 0B1 \mid 01$
	$\colorbox{purple}{C} \rightarrow 1C0 \mid 10$

4. Convert all other rules
4.
$$
\begin{align}
	\mathtt{S} &\rightarrow \mathtt{\mathtt{0B1|01|1C0|10}|\epsilon}\\
	\mathtt{A} &\rightarrow \mathtt{0B1|01|1C0|10}\\
	\mathtt{B} &\rightarrow \mathtt{0B1|01}\\
	\mathtt{C} &\rightarrow \mathtt{1C0|10}\\
	\mathtt{N_1} &\rightarrow \mathtt{B1}\\
	\mathtt{M_1} &\rightarrow \mathtt{0}
\end{align}
$$



  
4 ex)
$$
\begin{align}
	\mathtt{V} &\rightarrow x_1x_2x_3\dots x_k\\
	\mathtt{BECOMES}\\
	\mathtt{V} &\rightarrow x_1N_1\\
	\mathtt{N_1} &\rightarrow \mathtt{0B1|01}\\
	\mathtt{N_2} &\rightarrow \mathtt{1C0|10}
\end{align}
$$



DEF (summarized Chomsky Normal Form):
allowed rules like


$A\rightarrow BC$ or $A\rightarrow a$
where BC are not start variables
and the start variable can be empty string

THEOREM:
Any CFL can be generated by a CFG in Chomsky Normal Form


*The proof introduces things that are not allowed in Chomsky Normal Form but we deal with it later*

PROOF:
Supposed A is a CFL and let G be a CFG that generates A.

Add $S_0$ a new start variable along with the rule $S_0\rightarrow S$ Where S is G's start variable.

Next, remove $\epsilon$ rules of the form $A\rightarrow \epsilon$ when A is not $S_0$.

For $R\rightarrow uAv$, add $R\rightarrow uv$ 
For $R \rightarrow uAvAw$,add $R\rightarrow uvAw$, $R\rightarrow uAvw$, and $R\rightarrow uvu$.
For $R\rightarrow A$, add $R\rightarrow \epsilon$ unless it had previously been removed. **Otherwise you would get an infinite loop**

Repeat until all $\epsilon$ rules have been removed.

Next, we remove all unit rules $A\rightarrow B$.
If $B\rightarrow u$, add $A\rightarrow u$ unless this was a unit rule previously removed.

Repeat until there are no unit rules.

Replace $A\rightarrow u_1u_2u_3\dots u_k$ with 
$A\rightarrow u_1N_1$
$N_1\rightarrow u_2N_2$
$N_2\rightarrow u_3N_3$
$N_{k-3}\rightarrow u_{k-2}N_{k-2}$
$N_{k-2}\rightarrow u_{k-1}u_{k}$

Replace any terminal $u_i$ in the preceding rules with a new variable $U_i\rightarrow u_i$



DEF:
A pushdown autamaton (PDA) is 6-tuple $(Q,\Sigma,\delta,q_0,F)$
where $Q,\Sigma,$ are finite sets and
- $Q$ is the set of states
- $\Sigma$ is the input alphabet,
- handman looking symbol is the stack alphabet,
- $\delta:Q\times (\Sigma \cup \{\epsilon\}) \times (hangman\cup \{\epsilon\}) \rightarrow powerset (Q\times (hangman \cup \{\epsilon\}))$ is the transition function
- $q_0 \elementof Q$ is the start state, and
- $F \subset Q$ is the set of accept states
- 
# Pushdown Automata

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
      \node[state, initial, accepting] (1) {$q_1$};
      \node[state] (2) [right =of 1] {$q_2$};

      \draw (1) edge[right] node {$0$} ()
                edge[loop right] node {$1$} ();
    \end{tikzpicture}
\end{document}
```
$M_{1}= (Q,\Sigma, \Gamma, \delta, q_{1}, F)$ where:
- $Q=\{q_1,q_2,q_3,q_4\}$
- $\Sigma=\{0,1\}$,
- $\Gamma=\{0,\$\}$,
- $F=\{q_{1,}q_4\}$, and
- $\delta$ is given by:


| input | 0           | 0           | 0             | 1                    | 1           | 1           | $\epsilon$  | $\epsilon$           | $\epsilon$     |
| ----- | ----------- | ----------- | ------------- | -------------------- | ----------- | ----------- | ----------- | -------------------- | -------------- |
| stack | 0           | $           | $\epsilon$    | 0                    | $           | $\epsilon$  | 0           | $                    | $\epsilon$     |
| $q_1$ | $\emptyset$ | $\emptyset$ | $\emptyset$   | $\emptyset$          | $\emptyset$ | $\emptyset$ | $\emptyset$ | $\emptyset$          | $\{(q_2,\$)\}$ |
| $q_2$ | $\emptyset$ | $\emptyset$ | $\{(q_2,0)\}$ | $\{(q_3,\epsilon)\}$ | $\emptyset$ | $\emptyset$ | $\emptyset$ | $\emptyset$          | $\emptyset$    |
| $q_3$ | $\emptyset$ | $\emptyset$ | $\emptyset$   | $\{(q_3,\epsilon)\}$ | $\emptyset$ | $\emptyset$ | $\emptyset$ | $\{(q_4,\epsilon)\}$ | $\emptyset$    |
| $q_4$ | $\emptyset$ | $\emptyset$ | $\emptyset$   | $\emptyset$          | $\emptyset$ | $\emptyset$ | $\emptyset$ | $\emptyset$          | $\emptyset$    |
