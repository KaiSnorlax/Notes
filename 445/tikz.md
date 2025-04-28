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


