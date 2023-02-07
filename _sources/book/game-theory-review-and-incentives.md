# Game Theory Review + Incentives

## Game Theory and Mechanism Design

Classical game theory analyzes strategic behavior:
* Given a strategic environment (a "game"), what can we say about the likely outcome?
* Mechanism design flips the problem around
* How can we create rules of play (a "mechanism") so that even if players are strategically sophisticated,
    we still get a desired outcome?


```{glossary}
game
    A game in a strategic form is a triple $(N, A, u)$ consisting of:
    * A set of players $N = \{1, \ldots, n\}$
    * Possible _actions_ for each player: $A_1, \ldots, A_n$
    * Payoff functions for each player: $u_i(a_1, \ldots, a_n)$ for $u: A_1 \times \dots \times A_n \to
    \mathbb{R}^n$


dominant action
    Action $a_i$ is (weakly) _dominant_ for player $i$ if for all $a_i'$ and $a_{-1}$: $u_i(a_i, a_{-1}) \geq u_i(a_i', a_{-i})$ and for some $\hat{a}_{-i}$, $u_i(a_i, \hat{a}_{-i}) > u_i(a_i', \hat{a}_{-i})$.
```

```{tip} Intuition
It's a no-brainer for $i$ to play a dominant action if she has one; it is an optimal choice _regardless of how the others may play_.
```

```{glossary}
Nash equilbrium
    Action profile $a = (a_1, \ldots, a_n)$ is a _Nash equilibrium_ if for each player $i$ and action $a_i'$, $U_i(a_i, a_{-i}) \geq u_i(a_i', a_{-1})$. In words, an action profile $a$ is a Nash equilibrium if no player $i$ can increase its own payoff above $u_i(a)$ by unilaterally changing in its action from $a_i$ to some other action $a_i'$.
```


### Incomplete Information
* What happens if the players don't know each other's payoff functions? For example, in an auction, players may
not know the other bidders' valuations.
* (Bayesian) Nash equilibrium is more subtle: each player's optimal choice depends on what it believes others' payoffs may be,
so each player's expected payoff depends on probabilities of what others would do with different payoffs.

### Allocation Problems

An allocation problem consists of player $i = 1, \ldots, n$, a set of possible outcomes or allocations $X$, and
(possibly) payments by each player $p_1, \ldots, p_n$, and value functions $v_i(x)$ such that the payoff for each
player is $v_i(x) - p_i$.
Challenge:  the _mechanism designer_ typically does not know the payoff functions! The function is the player's privately known "type."

#### "Good" Allocations
Various criteria may define "good" allocations or outcomes. In auction problems, a good allocation might be one that is _Pareto efficient_ given everyone's values, or one that has high revenue for the seller. In matching problems, a good allocation might be one that is _stable_.

### Mechanisms

```{glossary}
mechanism
    A mechanism $(M, x, p)$ is a triple consisting of:
    * A set of possible _messages_ for each player: $M_1, \ldots, M_n$
    * An allocation rule: $X(m_1, \ldots, m_n)$
    * Possibly: a payment rule $p: M_1 \times \ldots \times M_n \to \mathbb{R}^n$ where player $i$ pays $p_i(m_1, \ldots, m_n)$.

    We will look at mechanisms with and without payments. If there are no payments, set all $p_i \equiv 0$.

matching mechanism
    A **matching mechanism** is a mapping from **reported** preferences into a matching. (no payments)

truthful mechanism
    A mechanism is **truthful** if truthful reporting is a dominant acution for each participant.

```

#### Example 1: Gayle-Shapley Marriage Problem
In the Gale-Shapley marriage problem, the messages are statements of preference (not necessarily truthful). The outcome/allocation/assignment is a matching, which the mechanism selects as a function of the reported preferences. No payments are made. A "type" is the preference list of each agent.

#### Example 2: Simple Auction
In a simple auction problem, the messages are the bids $(b_i \geq 0)$. The auction mechanism determines who wins and what everyone must pay as a function of the bids. A type is typically a person's value (maximum price).

A mechanism plus payoffs defines a game. The possible actions are the messages: $M_1, \ldots, M_n$. The payoffs are functions of the messages $u_i(m_1, \ldots, m_n) = v_{i}\left(x\left(m_{1},\ldots,m_{n}\right)\right) - p_i(m_1, \ldots, m_n).$

Often, we will focus on _direct mechanisms_: $M_i$ is equal to the set of $i$'s possible payoff functions (or preferences).

```{glossary}
strategy-proof mechanism
    A _strategy/action_ for player $i$ specifies what message to send as a function of player $i$'s type. A mechanism is _strategy-proof_ if each player $i$ has a dominant strategy, that is, a strategy that is optimal regardless of the strategies chosen by the other players. Sometimes, we'll look at mechanisms that are not strategy-proof, using Nash equilibrium to forecast mechanism outcomes.
```

### Applying GT to Market Design

#### Studying existing markets
Identify the "rules of the game," the incentives for participants, and how they behave. Then try ot understand why the market functions well, or not so well.

#### Designing new markets
Identify the economic problem to be solved, the players and their incentives and information. Then try to understand what sort of market rules would lead to a good outcome when participants are selfish and smart.

Economic theory provides a conceptual framework, but good practice also uses data and experiment to test hypotheses and identify things models may have missed.

## Incentives in Matching

```{admonition} Question
Can stable matching mechanisms be truthful?
```

### From Algorithms to Mechanisms

Algorithm analysis assumes that inputs are given and correct. Mechanism analysis also examines the inputs and asks:
* Is the mechanism truthful?
* Is it easy for participants to know what to report?


```{prf:theorem} Man-Proposing Mechanism is Truthful for Men
:label: Man-Proposing-Truthful
The direct mechanism that selects the man-optimal stable allocation using reported values (for example by running the man-proposing deferred acceptance algorithm) is truthful for the men.
```

```{prf:proof}
Suppose man $m$ makes report $r$ that (fixing others' reports) leads to matching $x$ in which $m$ is matched to woman $w$: $\mu_x(m) = w$. If instead of reporting $r$, $m$ reports that $w$ is his only acceptable woman, $x$ is still an acceptable stable matching to all parties. By the {prf:ref}`rural hospitals theorem<rural-hospitals>`, $m$ is matched in every stable matching with the revised report. Since $w$ is the only acceptable woman, {prf:ref}`DAA<daa>` matches $m$ to $w$. 

A key observation is that since $m$ is matched in every stable matching, any acceptable matching $y$ in which $m$ is unmatched must be blocked by either $(m, w)$ or some $(m', w')$ with $m \neq m'$.

Suppose that instead of reporting that only $w$ is acceptable, $m$ makes a "truncated truthful report" meaning that the women are ordered truthfully but those ranked below $w$ are reported to be unacceptable. As before, $m$ is matched in every stable matching even with the truncated report. Say the DAA now matches $m$ to woman $w'$ where $w' \succ_m w$. 

Say that $m$ had just reported truthfully, then the DAA would select the man-optimal stable matching $\hat{x}$. Any matching that was blocked or unacceptable with the truncated report is still blocked or unacceptable in the same way. Hence $\hat{x}$ is still the man-optimal stable matching and $\mu_{\hat{x}(m) = w'}$.

Putting it all together, we get that for *any* reports by the women and the other men, if man $m$ reports truthfully instead of reporitng $r$, he will be matched to woman $w'$ instead of to woman $w$ where $w' \succ_m w$.
```

```{admonition} Exercise
1. Show that truthful reporting is a weakly dominant action for the men.
2. Which steps of the proof also apply to women (in the man-offering deferred acceptance algorithm)?
3. What can you infer about the structure of women’s optimal reports when they play strategically?
```

