# Matching Theory

## Two-Sided Matching

### Problem Statement

Two different kinds of parties to be matched. Participants of both kinds care about to whom they are matched. Money and prices can't be used to guide the match.

### Sample Applications

* School assignment
* College admissions
* Medical residencies
* Heterosexual marriage & dating markets
* Judicial clerkships
* Frat/Sorority "rush"
* Job assignment in firms
* Military postings

## Marriage Model

### Participants of Two Kinds

A set of men $M$ and women $W$.
A set of men $M$ with typical man $m \in M$ and a set of women $W$ with typical woman $w \in W$. We assume one-to-one matching. Each man can be matched to one woman or remained unmatched and vice versa. People have strict preferences over their potential partner. A man $m$ is "acceptable" to a woman $w$ if she prefers him to being unmatched. We define an "acceptable" woman similarly.

```{glossary}
matching
    A matching is a set of pairs of the form $(m, w)$ or self-matching $(m,m)$ or $(w, w)$ such that each individual appears in exactly one pair. 
```

```{admonition} Notation
If the match includes $(m, m)$ then $m$ is unmatched. Similarly, $(w, w)$ means $w$ is unmatched.
```

```{glossary}
blocking pair
    Given a matching $\mu$, a blocking pair $(m, w)$ is a man $m$ and a woman $w$ who would both prefer to match with each other rather than to their assigned partners in that matching.

unstable matching
    A matching is unstable if either:
        1. Some individual is matched to an unacceptable partner, or 
        2. There is blocking pair $(m, w)$ – that is, a man $m$ and a woman $w$ who are not matched, yet each prefer the other to their current partner in the matching.

stable matching
    If a matching isn't unstable, it's stable.
```

#### Question

There are two men $m, m'$ and two women $w, w'$.

* $m$ prefers $w$ to $w'$ to $m$ ($w \succ_m w' \succ_m m$)
* $m'$ prefers $w'$ to $w$ to $m'$
* $w$ prefers $m$ to $m'$ to $w$
* $w'$ prefers $m'$ to $m$ to $w'$

How many matchings are possible? Which are stable and which are unstable? Why?

```{dropdown} Solution
There are seven possible matchings:
1. $\{(m, w), (m', w')\}$
2. $\{(m, w), (m', m'), (w', w')\}$
3. $\{(m, w'), (m', w)\}$
4. $\{(m, w'), (m', m'), (w, w)\}$
5. $\{(m, m), (m', w'), (w, w)\}$
6. $\{(m, m), (m', w), (w', w')\}$
7. $\{(m, m), (m', m'), (w, w), (w', w')\}$

Clearly, any matching containing a self-match is unstable because everyone prefers _someone_ to _no one_. $\{(m, w'), (m', w)\}$ is also unstable because $(m, w)$ is a blocking pair. Thus, $\{(m, w), (m', w')\}$ is the unique stable matching.
```

```{attention}
Get more practice [here](https://colab.research.google.com/drive/1ca7I3ArNiOGom9U0re6zPYyIi781W65V?usp=sharing)!
```

#### Challenge Question

If we have $|M| = |W| = n$, how many matchings are possible? What about when $|M| \neq |W|$? How does this change if we no longer assume strict preferences? How do we define "blocking pairs" if we give up strict preferences?

## Deferred Acceptance Algorithm

```{index} Deferred Acceptance Algorithm (DAA)
```

### Algorithm

```{prf:algorithm} Deferred Acceptance Algorithm (DAA)
:label: daa
1. Men and women rank all potential partners.
2. Each man proposes to the highest-ranked acceptable woman on his list, or to nobody if no one on the list is acceptable.
3. Each woman holds only her most preferred acceptable proposal and rejects all others.
4. Each $m$ who is rejected by a woman removes her from his list.
5. Repeat 2-4 until no man is rejected. If no man is rejected, then each woman "accepts" her offer and is matched to the man whose proposal she holds.
```

This is the _"man-proposing"_ deferred acceptance algorithm; there is also a _"woman-proposing"_ version.

### Existence

```{prf:theorem} Stable Matchings Exist
:label: stable-matchings-exist
The deferred acceptance algorithm ends in finite time with a stable matching. (In particular, a stable matching exists).
```

```{prf:proof}
The algorithm must end in a finite number of rounds. Suppose $m$ and $w$ are matched. Each must be acceptable to the other. (Why?) There is no blocking pair $(m, w')$ because if $m$ prefers $w'$ to $w$, then (1) at some time, $m$ _had_
proposed to $w'$ and she eventually rejected him. Either $m$ is unacceptable to $w'$ or she then held a man she preferred to $m$. At every later round, $w'$ held the same man or some more preferred one, so $w'$ prefers her final match to $m$. Therefore, there are _NO BLOCKING PAIRS_. $\blacksquare$
```

## Optimality

Man-Optimal
: A stable matching is _man-optimal_ if every man prefers his partner to any partner he could possibly have in any stable matching.

```{prf:theorem}
The man-proposing DA algorithm produces the man-optimal stable matching.
```

```{prf:proof}
We say that $w$ is _possible_ for $m$ if $(m, w)$ is in some stable matching. Show _by induction_ that no man is ever rejected by a woman who is possible for him. True at round 0. Suppose this is the case through round $n$ of the algorithm. Suppose at round $n+1$, woman $w$ rejects $m$ in favor of $m'$. Note, this means $m'$ made an offer to $w$ in round $n+1$ and hence all the women whom $m'$ prefers to $w$ have rejected him and so, by the inductive hypothesis, must be impossible for him. We claim that $w$ must be _impossible_ for $m$. Suppose to the contrary that $w$ is possible for $m$ and consider the stable matching $X$ that includes $(m, w)$ and $(m', w')$ for some $w'$. By the inductive hypothesis, $m'$ must prefer $w$ to $w'$. But then $(m', w)$ blocks $X$, so $X$ is not stable. So in no round of the man-proposing DA is any man rejected by a possible woman. $\blacksquare$
```

Pessimal Stable Matchings
: A stable matching $X$ is _woman-pessimal_ if every woman prefers her partner at every other stable matching to her partner at $X$.

```{prf:theorem}
The man-proposing DA produces the woman-pessimal stable matching.
```

```{prf:proof}
We have already shown that the outcome $X$ of the man-offering algorithm is a man-optimal stable matching. We must show that any other matching $X'$ is better for all the women whose partners have changed.Suppose that woman $w$ is matched to $m$ at $X$ and to a different man $m' \neq m$ at another stable matching $X'$. Suppose $m$ is matched to woman $w'$ in the matching $X'$. Since $X$ is man-optimal, $m$ prefers $w$ to $w'$. But since $X'$ is stable, it is not blocked by $(m, w)$, so $w$ must prefer $m'$ to $m$. $\blacksquare$ 
```

### Better-than-Optimal Matchings

The man-optimal stable matching is best for men _among stable matchings_, but there may be unstable matchings that all men weakly prefer and some strictly prefer.

#### Example

Say we have three men and two women.

Man Preferences:

* $m_1: w_1 \succ w_2$
* $m_2: w_2 \succ w_1$
* $m_3: w_1 \succ w_2$

Woman Preferences:

* $w_1: m_2 \succ m_3 \succ m_1$
* $w_2: m_1 \succ m_3 \succ m_2$

What is the unique stable matching? Are there any matchings that all men weakly prefer?

```{dropdown} Solution
The unique stable matching is $\{(m_1, w_2), (m_2, w_1), (m_3, m_3)\}$, but _men_ would be better off if $m_1$ and $m_2$ could swap partners.
```

```{admonition} Lesson
Stability respects women's preferences as well as men's. The distinction will be important when we discuss school choice if we want to prioritize student preferences over school's preferences.
```

## Rural Hospitals Theorem

Why "rural hospitals?" Deferred acceptance is used to assign doctors to hospitals—some hospitals wondered if changing the algorithm would help them fill positions.

```{prf:theorem} Rural Hospitals Theorem
:label: rural-hospitals
The sets of men and women who are unmatched is the same in _all_ stable matchings.
```

```{warning}
This does not mean that the matchings are the same, just that the sets of men and women who are matched or unmatched is the same across all stable matchings.
```

```{prf:proof}
Let $M, W$ be the _sets_ of men and women matched in the man-optimal stable matching (which is also woman-pessimal). Let $M', W'$ be the _sets_ of men and women matched in some other stable matching. We seek to show that $M = M'$ and $W = W'$. Any man in $M'$ must also be matched in the man-optimal stable matching, so $M' \subseteq M$ $\ldots$ and also $|M'| \leq |M|$.  Similarly, since any woman in $W$ is no worse off in the alternative matching, $W \subseteq W'$ $\ldots$ and also $|W| \leq |W'|$. In any feasible matching, the number of matched men equals the number of matched women, so $|M| = |W|$ and $|M'| = |W'|$. We have: 
\begin{align*}
\left|M'\right|\le\left|M\right|=\left|W\right|\le\left|W'\right|=\left|M'\right|,
\end{align*}
so all these are equal. Adding together that $M' \subseteq M$ and $W' \subseteq W$, we must have some $M=M'$ and $W=W'$. $\blacksquare$
```
