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

# Lecture 3: NFAs
**DEF**: NFA (non-deterministic finite automota) is a 5 tuple 
$$M = (Q, \Sigma, \delta, q_0, F)$$
Similar to a DFA. 

An NFA accepts a string $x \in \Sigma^*$ if there exists $r_0, ..., r_n \in Q$ s.t.
1. $r_0 = q_0$
2. $r_1 \in \delta(r_{i-1}, q_i)$
3. $r_n \in F$

**THM**: For any NFA $M$, there exists a DFA $M'$ such that 
$$\mathcal{L}(M) = \mathcal{L}(M')$$

**PRF**: 
Let $M = (Q, \Sigma, \delta, q_0, F)$. 

We construct $M' = (Q', \Sigma, \delta', q_0', F')$

Let 
1. $Q' = P(Q)$
2. $q_0' = \{q_0\}$
3. $F' = \{S \subseteq Q: S \cap F \neq \empty \}$
4. $\delta'(S, a) = \bigcup_{q \in S} \delta(q, a)$

**DEF**: An $\epsilon$-NFA is an NFA with $\epsilon$ transitions (one which allows transition to a new state without reading any input.)

**THM**: For any $\epsilon$-NFA M, there exists a DFA $M'$ such that 
$$\mathcal{L}(M) = \mathcal{L}(M')$$

**PRF**: We construct 
$$M' = (Q', \Sigma, \delta', q_0', F')$$
Let
1. $Q' = P(Q)$ (power set of $Q$)
2. $q_0' = \epsilon-closure(\{q_0\})$
3. $F' = \{S \subseteq Q: S \cap F \neq \empty\}$
4. $\delta'(S, a) = \bigcup_{q \in S} \epsilon - closure (\delta(q, a))$

**THM**: If $A$ is regular then $A^R$ is regular (reversal).

**PRF**: Since $A$ is regular, $A$ has an $\epsilon$-DFA $M$ s.t. $A = L(M)$. 

Now we can just reverse all the arrows. Now make the starting states the final states and the final states the starting states. 

**THM**: Pumping Lemma

For every regular language $L$, there exists $p \geq 0$, such that for any $s \in L$ of length at least $p$, we can write $s = xyz$ where 
1. $|y| > 0$
2. $|xy| \leq p$
3. $xy^kz \in L$ for all $k \geq 0$ 

**PRF**: Since $L$ is regular, there exists $(M = (Q, \Sigma, \delta, q_0, F))$ such that $L = \mathcal{L}(M)$. 

Take $p = |Q|$
Given $s \in L \Rightarrow \exists r_0, ..., r_n \in Q$ where
- $r_0 = q_0$
- $r_i = \delta(r_{i-1}, s_i)$
- $r_n \in F$

The idea is that since the length of the string is larger than the number of states there has to be a loop where the sequence of states has to have a duplicate. This loop can be repeated infintely or not at all. to accept a new string with an arbitrary amount of the characters encompassed by the loop.

# Lecture 4: Nonregular languages

We can use the pumping lemma to disprove things
e.g.

**THM**: $L = \{0^m1^n : m \neq n\}$ is not regular

**PRF**: given $p$, take $s= 0^p1^{p+p!}$

We can also do a proof by contradiction

**PRF**: suppose $L$ is regular. Then $\bar{L}$ is regular. Thus, 

$\bar{L} \cap 0^*1^*$ must also be regular. 

$$
\begin{align*}
L \cap 0^*1^* &= \{0^a1^a\}
\end{align*}
$$
which is not regular.

## Myhill-Nerode thm
**DEF**: Given $L \subseteq \Sigma^*$ .
We say $x, y \in \Sigma^*$ are $\dot{L}$-equivalent$ ($x \equiv_L y$) if for all $z \in \Sigma^*$,

$$ xz \in L \iff yz \in L$$

**EX**: for $L$ = {bitstrings which start and end with the same symbol} we have 5 equivalence classes where every element is equivalent

1. {$\epsilon$}
2. {bitstrings that start and end with 0}
3. {bitstrings that start and end with 1}
4. {bitstrings that start with 0 and end with 1}
5. {bitstrings that start with 1 and end with 0}

**THM** Myhill Nerode
A language is regular if and only if there are finitely many equivalence classes of $\equiv_L$

**PRF**: ($\Rightarrow$)
Let $M$ be a DFA recognizing $L$. First, assume that all states are reachable. 

For each $q \in Q$ 
$$
\{\text{The set of input strings where the DFA transitions from $q_0$ to $q$}\} \subseteq \text{all equivalence classes}
$$

Thus there are at most $|Q|$ equivalance classes (and therefore it is finite)

($\Leftarrow$)
Build an automaton $M = (Q, \Sigma, \delta, q_0, F)$

out of equivalence classes ($q \in Q$ is an equivalence class)

Let $q_0 = \{\text{equivalence class for }\epsilon\}$

$\delta(S, a) = $ eq class containing $xa$ for any $x \in S$ 

## Minimization (Moore's / Hoperoft's)
Minimization take the following steps:
1. Remove unreachable states
2. Assume all state in some equivalence class. Split them into a class of accepting and non-accepting state sets
3. Split sets until they're deterministic based on the input

# Lecture 5: Turing machines

**DEF**: Turing Machine

A deterministic one-tape TM is a 7=tuple 
$$(Q, \Gamma, b, \Sigma, \delta, q_0, F)$$
Where

1. $Q$ is a finite set of states
2. $\Gamma$ is the tape alphabet
3. $b \in \Gamma$ is the blank symbol
4. $\Sigma \subseteq \Gamma \backslash {b}$ is the input alphabet
5. $\delta: (Q \backslash F) \times \Gamma \rightarrow Q \times \Gamma \times \{L, R\}$ is the transition function. (i.e. takes a state and a letter of the alphabet and produces a new state, a letter to write and which direction to move) 
6. $q_0 \in Q$ is the initial state
7. $F \subseteq Q$ is the final state

**DEF** Configure of a TM

A configuration of a TM is 
- the state ($q \in Q$)
- The contetns of the tape ($wy \in \Gamma^*$)
- The position of the tape head

We write this $wqy$ the tape head is in state $q$ at the first symbol of $y$. 

We assume that all but finitely many symbols are blank.

The initial configuration on input $x \in \Sigma^*$ is 
$$\epsilon q_0 x$$

The final configuration is 
$$wqy$$
with $q \in F$

**DEF** A config $waqby$ yields a config $wracy$ where $w, y \in \Gamma^*$, $a, b, c \in \Gamma$ and 

$$\delta(q, b) = (r, c, L)$$

We write $waqby \vdash wracy$.

**DEF** Halting:

We say the TM halts on input $x \in \Gamma^*$ if there exists configigurations $c_0, ..., c_n$ 

1. $c_0$ is $\epsilon q_0 x$
2. $\forall i, c_i \vdash c_{i+1}$
3. $c_n$ is a final configuration

Otherwise, it loops. 

**DEF** Accpeting a language:

e say a TM recognizes a language if it halts on $x \in \Sigma^*$ iff $x \in L$

**DEF** Decides:

$$F = \{q_{\text{accept}}, q_{\text{reject}} \}$$

Define an accepting configuration is a final config with $q = q_{\text{accept}}$. Likewise for a rejecting config.

We say a TM decides a language $L \subseteq \Sigma^*$ if it accepts $x \in \Sigma^* \iff x \in L$. 

**DEF** R, RE

R is the set of all languages where there exists a TM which decides the langauge 

RE is the set of all languages where there exists a TM which recognizes the language

$$R \subseteq RE$$

