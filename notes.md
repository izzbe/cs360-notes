# Lecture 1: Intro

**THM**: For $X$ a finite set with $k$ elements, there exists a one-to-one function 
$$h: X \rightarrow \{0,1\}^{\lceil \log k \rceil}$$

**THM**: There is a bijection between $\{0, 1\}^*$ and $\mathbb{N}$

**THM**: THere is no onto function
$$f: X \rightarrow P(X)$$
Where P is the powerset of $X$

# Lecture 2: Finite automata

**DEF**: A deterministic finite automaton (DFA) is a 5-tuple 
$$(Q, \Sigma, \delta, q_0, F)$$
Where

- $Q$ is a finite set of states
- $\Sigma$ is a finite alphabet
- $\delta: Q \times \Sigma \rightarrow Q$ a transition function
- $q_0 \in Q$ The initial state
- $F \subseteq Q$ the set of accepting states

We say that $M$ accepts $x = x_1, ..., x_n \in \Sigma^*$ If there exists a sequence of states $r_0 , ..., r_n \in Q$ such that 
1. $r_0 = q_0$
2. $r_1 = \delta(r_{i-1}, q_i)$ for i= 1,..., n
3. $r_n \in F$

We also say that $M$ recognizes the language 
$$\mathcal{L}(M) = \{x \in \Sigma^* : M \text{ accepts } x\}$$

**DEF**: A language is regular if there exists a DFA which recognizes it.

**THM**: If $A \subseteq \Sigma^*$ is a regular language, then so is the complement 
$$\bar{A} = \Sigma^* \backslash A$$
**PRF**:
Since $A$ is regular, $\exists$ a DFA 
$$M = (Q, \Sigma, \delta, q_0, F)$$
which recognizes it. 
Construct 
$$M' = (Q, \Sigma, \delta, q_0, Q \backslash P)$$
Say $x=x ,..., x_n \in \Sigma^*$ but $x \not \in A$
There exists $r_0,...,r_n \in Q$ such that
1. $r_0 = q_0$
2. $r_i = \delta(r_{i-1}, q_i)$

Thus,
$$
\begin{align*}
x \not \in A &\iff r_n \not \in F
\\
&\iff r_n \in Q \backslash F
\\
&\iff M' \text{ accepts } x
\end{align*}
$$

**THM**: If $A, B \subseteq \Sigma^*$ are regular then $A \cap B$ is regular.
**PRF** Since A, B are regular $\exists$
$$
M_A = (Q_a, \Sigma, \delta_A, q_a, F_A)
\\
M_B = (Q_B, \Sigma, \delta_B, q_B, F_B)
$$
We construct
$$
M_{A \cap B} = (Q_A \times Q_B, \Sigma, \delta_{A \cap B}, F_{A \cap B})
$$
Where 
- $\delta_{A \cap B}((r, s), x) = (\delta_A(r,x), \delta_B(s, x))$
- $q_{A \cap B} = (q_A, q_B)$
- $F_{A \cap B} = F_A \times F_B$

**THM**: If $A, B$ are regular, then $A \cup B$ are regular.

**PRF**: same as above but take $F_{A \cup B} = Q_A \times F_B \cup F_A \times Q_B$.

Or apply demorgans law with above.

**THM**: If $A, B$ are regular, then 
- $AB = \{ab : a \in A, b \in B\}$
- $A^* = \{a_1...a_n : n \geq 0, a_1, ..., a_n \in A\}$ 
- $A^R = \{a^R: a \in A\}$ (reversal operation)

Are all regular

**DEF**: Non deterministic finite automaton (NFA) is a 5-tuple 
$$(Q, \Sigma, \delta, q_0, F)$$
where
- $Q, \Sigma, q_0, F$ are the same as the DFA
- $\delta: Q \times \sigma \rightarrow \mathcal{P}(Q)$ (the transition function maps to a set of states)

An NFA accepts $x \in \Sigma^*$ if there exists a seq of states $r_0, ..., r_n$ such that

1. $r_0 = q_0$
2. $r_i \in \delta(r_{i-1}, x_i)$ for all $i$
3. $r_n \in F$ 
