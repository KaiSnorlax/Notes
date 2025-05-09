A finite automaton is a 5-tuple ($Q,\Sigma,\delta,q_{0},F$), where
1. $Q$ is a finite set called the states,
2. $\Sigma$ is a finite set called the alphabet,
3. $\delta: Q\times \Sigma \rightarrow Q$ is the transition function,
4. $q_{0}\in Q$ is the start state, and
5. $F \subseteq Q$ is the set of accept states.


A language is called a regular language if some finite automaton recognizes it.


Let $A$ and $B$ be languages. We define the regular operations union, concatenation, and star as follows:
- Union: $A \cup B = \{x \mid x \in A \mathtt{\ or\ } x \in B\}$
- Concatenation: $A \circ B = \{xy \mid x \in A \mathtt{\ and\ } y \in B\}$
- Star: $A^{*} = \{x_{1}x_{2}... \mid k \ge 0 \mathtt{\ and\ each\ } x_{i} \in A\}$


A nondeterministic finite automaton is a 5-tuple ($Q,\Sigma, \delta, q_{0},F$), where
1. $Q$ is a finite set called of states,
2. $\Sigma$ is a finite alphabet,
3. $\delta: Q\times \Sigma_{\epsilon} \rightarrow P(Q)$ is the transition function,
4. $q_{0}\in Q$ is the start state, and
5. $F \subseteq Q$ is the set of accept states.


Say that R is a regular expression if R is
1. $a$ for some $a$ in the alphabet $\Sigma$,
2. $\epsilon$,
3. $\emptyset$
4. ($R_{1} \cup R_{2}$), where $R_{1}$ and $R_{2}$ are regular repressions)
5. ($R_{1} \circ R_{2}$), where $R_{1}$ and $R_{2}$ are regular expressions, or
6. ($R_{1}^{*}$), where $R_{1}$ is a regular expression.
In items 1 and 2, the regular expressions $a$ and $\epsilon$ represent the languages {$a$} and {$\epsilon$}, respectively. In item 3, the regular expression $\emptyset$ represents the empty language. In items 4, 5, and 6 the expressions represent the languages obtained by taking the union or concatenation of the languages $R_1$ and $R_2$, or the star of language $R_1$, respectively.


A generalized nondeterministic finite automaton is a 5-tuple, ($Q,\Sigma, \delta, q_{start}, q_{accept}$), where
1. $Q$ is the finite set of states,
2. $\Sigma$ is the input alphabet,
3. $\delta: (Q-\{q_{accept}\}) \times (Q-\{q_{start}\}) \rightarrow R$ is the transition function,
4. $q_{start}$ is the start state, and
5. $q_{accept}$ is the accept state.


Pumping lemma:
If $A$ is a regular language, then there is a number $p$ (the pumping length) where if $s$ is any string in $A$ of length at least $p$, then $s$ may be divided into three pieces, $s = xyz$, satisfying the following conditions:
1. For each $i \ge 0, xy^{i}z\in A$,
2. $|y|\gt 0$, and
3. $|xy| \le p$.


A context-free grammar is a 4-tuple ($V, \Sigma, R, S$),  where
1. $V$ is a finite set called the variables,
2. $\Sigma$ is a finite set, disjoint from $V$, called the terminals,
3. $R$ is a finite set of rules, with each rule being a variable and a string of variables and terminals, and
4. $S \in V$ is the start variable.


A context-free grammar is in Chomsky normal form if every rule is of the form 
$$
\begin{align}
A &\rightarrow BC \\
A &\rightarrow a
\end{align}

$$
where $a$ is any terminal and $A,B$ and $C$ are any variavbles-except that $B$ and $C$ may not be the start variable. In addition, we permit the rule $S \rightarrow \epsilon$, where $S$ is the start variable.

A pushdown automaton is a 6-tuple ($Q, \Sigma, \Gamma, \delta, q_{0,}F$), where $Q,\Sigma, \Gamma$, and $F$ are all finite sets, and
1. $Q$ is the set of states,
2. $\Sigma$ is the input alphabet,
3. $\Gamma$ is the stack alphabet,
4. $\delta: Q\times \Sigma_{\epsilon}\times \Gamma_{\epsilon} \rightarrow P(Q\times \Gamma_{\epsilon})$ is the transition function,
5. $q_{0}\in Q$ is the start state, and
6. $F \subseteq Q$ is the set of accept states.


A deterministic pushdown automaton is a 6-tuple ($Q, \Sigma, \Gamma, \delta, q_{0}, F$), where $Q,\ \Sigma,\ \Gamma$, and $F$ are all finite sets, and
1. $Q$ is the set of states,
2. $\Sigma$ is the input alphabet,
3. $\Gamma$ is the stack alphabet,
4. $\delta: Q\times \Sigma_{\epsilon}\times \Gamma_{\epsilon} \rightarrow (Q\times \Gamma_{\epsilon}) \cup \{\emptyset\}$ is the transition function,
5. $q_{0}\in Q$ is the start state, and
6. $F \subseteq Q$ is the set of accept states.
The transition function $\delta$ must satisfy the following condition.
For every $q\in Q,a\in \Sigma$, and $x\in \Gamma$, exactly one of the values
$$\delta(q,a,x),\delta(q,a,
\epsilon),\delta(q,\epsilon,x) \mathtt{, and} \delta(q,\epsilon,\epsilon)$$
is not $\emptyset$.


A deterministic context-free grammar is a context-free grammar such that every valid string has a forced handle.


Prove that every NFA can be converted into an equivalent one that has a single accept state.

Let $N=(Q,\Sigma,\delta,q_0,F)$ be a NFA recognizing some language A

We will cfreate a new state 'F' to be our new accepting state.

For every previous accepting state, we add an epsilon transition from that state to the new state 'F'
Change previous accepting states into non-accepting styates




Prove if A is regular A^R is.


If A is regular then there is an NFA M that recognizes it