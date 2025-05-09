Give context-free grammars that generate the following languages. In all parts, the alphabet Σ is {0, 1}.
(a) {w | w starts and ends with the same symbol}
	S -> 0A0 | 1A1 | 1 | 0
	A -> S |

(b) {w | the length of w is odd and its middle symbol is a 0}
	S -> 0S0 |0S1 | 1S0 | 1S1 | 0

(c) {w | w = w^R, that is, w is a palindrome}
	S -> aSa | bSb | a | b | $\epsilon$




CFG to PDA 