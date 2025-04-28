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
Derivation for the string 123:
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
              child { node {$<DIGIT>$} }
              child { node {$<LITERAL>$} }
            }
          }
        }
      }
    };

\end{tikzpicture}
\end{document}
```

