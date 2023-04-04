# Stability, Order, and Unraveling

## History: Theory to Practice

The study of matching started as mathematics: first by Gale and Shapley (1962) who introduced the deferred acceptance algorithm, then others, including Stanford math Prof. Donald Knuth. In 1984, Al Roth made a surprising discovery. Since the 1950s, US hospitals have used a clearinghouse to assign graduating medical students to residencies. Students apply and interview at hospitals in the fall, then students and hospitals submit rank-order preferences in February. A computer algorithm is used to assign students to hospitals, and matches are all revealed on a single day: match day. Roth realized that the doctors has independently discovered and were using exactly the Gale and Shapley DA algorithm!

### National Residency Matching Program (NRMP)

History turns out to be illuminating. Into the 1930s, medical students found residencies through a completely decentralized process, but there were problems: students and hospitals made contracts earlier and earlier, eventually in second year of med school! Hospitals decided to change the system by adopting a centralized clearinghouse. The National Residency Matching Program (NRMP) was adopted, after various adjustments in 1952. The system has persisted but was modified in late 1990s to handle couples and some recent debate about salaries.

```{admonition} Question
Why might a centralized clearinghouse be useful? And how might the design of the clearinghouse matter?
```

### Stability and Orderly Markets

Some hypotheses to consider:

* Centralized clearinghouse can lead to more “orderly” market than decentralized (e.g., clinical psychology)
* Designing a clearinghouse to achieve a stable match might discourage re-contracting, or pre-contracting.

Are these hypotheses true? How can we test them?
Compare DA to alternative matching process.
Compare centralized markets to decentralized.
Ideally, with some sort of experiment (lab? natural?)

## Priority Matching

### Algorithm

```{prf:algorithm} Priority Matching
:label: priority-matching
1. Men and women submit their preferences.
2. Each man-woman pair gets a priority based on their mutual rankings.
3. An algorithm matches all priority 1 couples, takes them out of the market.
4. New priorities are assigned and process iterates.
```

```{admonition} Quesiton
Compared with DA, will priority matching lead to a stable matching? Should people be honest or strategic about their preferences?
```

#### Example

Find a stable matching.

Women Preferences:

* $w_1: m_2 \succ m_3 \succ m_1$
* $w_2: m_2 \succ m_3 \succ m_1$
* $w_3: m_2 \succ m_1 \succ m_3$

Men Preferences:

* $m_1: w_1 \succ w_2 \succ w_3$
* $m_2: w_3 \succ w_2 \succ w_1$
* $m_3: w_3 \succ w_1 \succ w_2$

```{dropdown} Solution
Man-Proposing DA:
```{list-table}
:header-rows: 1
* - Round 1
  - Round 2
  - Round 3
* - $m_1 \rightarrow w_1$
  - $m_1 \rightarrow w_1$ (rejected)
  - $m_1 \rightarrow w_2$
* - $m_2 \rightarrow w_3$
  - $m_2 \rightarrow w_3$
  - $m_2 \rightarrow w_3$
* - $m_3 \rightarrow w_3$ (rejected)
  - $m_3 \rightarrow w_1$
  - $m_3 \rightarrow w_1$
```

Find the outcome under the priority matching with order $1-1, 1-2, 1-3, 2-2, 2-3, 3-1, 3-2, 3-3$.

```{dropdown} Solution
Priority Matching with order $1-1, 1-2, 2-1, 1-3, 3-1, 2-2, \ldots$
1. Look for $1-1$ matches: $(m_2, w_3)$
2. Look for $1-2, 2-1$ matches among remaining: NONE
3. Look for $1-3$, $3-1$ matches among remaining: $(m_1, w_1)$
4. Look for $2-2$ matches among remaining: NONE
5. Look for $2-3$, $3-2$ matches among remaining: $(m_3, w_2)$
Unstable: $(m_3, w_1)$ is a blocking pair.  
```

### Failure of Priority Matching

Roth (1991, AER) studied residency matches in Britain, which are local and have used different types of algorithms --- a “natural experiment”.
Newcastle introduced priority matching in 1967. By 1981, 80% of the preferences submitted contained only a single first choice.
The participants had pre-contracted, before the formal market. This is the type of “market unraveling” that plagued the US residency market prior to the NRMP.
We’ll have more to say about unraveling later.

### Stability and Market Participation

Starting in the 1970s, an increasing number of couples graduated from medical school. Typically, couples want to be in the same city, but the DA algorithm doesn’t account for this; it might put a husband in Boston and wife in Chicago. So many couples started to go around the NRMP to find positions where they could be at the same hospital: match was threatened by a new form of unraveling. NRMP realized there was a problem and eventually asked Al Roth to redesign the match.

### Couples: A Problem

Couple $c = (c_1, c_2)$ and single student $s$. Two hospitals $h_1, h_2$ each hiring one student.

Preferences:

* $h_1: c_1 \succ s$
* $h_2: s \succ c_2$
* $s: h_1 \succ h_2$
* $c: (h_1, h_2)$ or nothing

There is no stable matching! Assign one member of couple? Then the couple will block. Assign $(h_1,c_1)$ and $(h_2,c_2)$? Then $h_2$ and $s$ block. Assign $(h_1,s)$? Then Couple and hospitals block. Assign $(h_2,s)$? Then $s$ and $h_1$ block.

#### Hospital-Offering DA Extension

```{list-table}
:header-rows: 1

* - Round 1
  - Round 2
  - Round 3
* - $h_1 \rightarrow c_1$ ($c_1$ rejects)
  - $h_1 \rightarrow s$
  - 
* - $h_2 \rightarrow s$ ($s$ holds)
  - ($s$ rejects $h_2$)
  - $h_2 \rightarrow c_2$ ($c_2$ rejects)
```

End State: $(h_1, s)$ match.

#### Student-Offering DA Extension

```{list-table}
:header-rows: 1

* - Round 1
  - Round 2
* - $c \rightarrow (h_1, h_2)$
  - $c_1$ "withdraws" from $h_1$
* - $s \rightarrow h_1$ ($h_1$ rejects)
  - ($h_2$ rejects $c_2$)
```

End State: $(h_2, s)$ match.

## NRMP Redesign

No “clean” solution to the couples problem. Student-proposing perhaps a bit better: switch from hospital to student proposing version of DA. What if DA algorithm doesn’t find a stable match? Perturb the algorithm and “keep going.” Not guaranteed to find a stable match, but seemed to work in simulations (and “large” markets). Similar theory-guided “fixes” brought couples back into the match, stopping the unraveling.

### Takeaway

NRMP is an unusual but illuminating design of a matching market because it is so organized.

* Motivation for moving to a clearinghouse was unraveling (i.e., disorderly operation) of decentralized matching.
* Design of the clearinghouse evidently quite important: systems with unstable matching seem to have fared poorly.

### Further Examples

* Medical fellowships
* judicial clerkships
* Investment bank hiring
* College football bowls
* NBA/NCAA basketball recruiting
* High school prom
* Political campaigns/primaries
* College admissions

## Timing Problems

Decentralized markets with fixed appointment dates can have timing issues that may create problems

* Employers and workers may have an incentive to **“jump the gun”** in order to ensure a match or a good match.
* Employers may be hesitant to leave offers outstanding, and may want to use **“exploding offers”** to rush decisions.
* The market can clear in a disorderly fashion so that participants end up with a relatively **limited set of choices**.

```{glossary}
exploding offer
  An offer with a response deadline before the official close of the market (i.e., before the agent can expect to receive all potential offers).
```

Different markets have tried to address these problems in various ways, with varying success (!).

## Matching Design

Well-designed matching markets aim for several goals:

1. Orderly process for making matches: ability to consider options, not be rushed into making decisions, coordinated timing.
2. Good incentives: truthfulness, makes sense to participate, no desire to re-contract or side contract to avoid market outcome.
3. Good outcomes: efficient, stable, matching.

Factors we have identified as important include: the matching algorithm (DA vs. priority), preferences of participants (couples vs. singles), culture and ability to enforce rules (exploding offers vs. patience), broader environment (admission rates).
