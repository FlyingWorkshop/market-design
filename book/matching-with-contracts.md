# Matching with Contracts

## Extended Marriage Problem

Preferences in matching often involves additional terms besides just your partner’s identity:
Dating: Will we go to the concert or the ball game, alone or with others, etc.
College admissions: Whose lab will the student work in? Is financial aid offered?
Marriage: “Let’s have kids right away and take over dad’s store in Provo, Utah” or “Let’s travel abroad for a year and then live in a commune in Portland, OR.”

### Formulation

There is a finite set of terms ${T}$ with typical element $t \in {T}$. Each man $m$ has a strict ranking of pairs of the form $(w,t)$ or "unmatched". Each woman $w$ has a strict ranking of pairs of the form $(m,t)$ or "unmatched". A triple $(m,w,t) \in {M} \times {W} \times {T}$ is called a contract. Think of a contract form that has two blank lines and a series of check boxes. One writes the names of the contracting parties $m$ and $w$ into the lines and checks boxes to determine contract options or terms.

### Stability

```{glossary}
matching (contracts)
    A matching is a function $\mu : M \cup W \rightarrow (M \cup W) \times T$ such that $\mu(m) \in (W \cup \{m\}) \times T$ and $\mu(w) \in (M \cup \{w\}) \times T$, and $\mu(m) = (w,t) \Leftrightarrow \mu(w) = (m,t)$. The same $t$ can appear in multiple contracts in $\mu$.

unstable matching (contracts)
    A matching $\mu$ is unstable if:
    1. Some contract $(m,w,t)$ is unacceptable to either $m$ or $w$, or
    2. There is some blocking contract $(m',w',t')$ that $m$ and $w$ both prefer to their $\mu$-contract.

stable matching (contracts)
    A matching $\mu$ is stable if it is not unstable.
```

### Extended Man-Offering Algorithm

```{index} extended man-offering DAA
```

```{index} extended woman-offering DAA
```

```{prf:algorithm} Extended Man-Offering Algorithm
:label: extended-man-offering-daa
**Inputs** Each man and woman submits a preference list ranking the possible partner-terms pairs.

1. Each man offers the highest remaining acceptable "contract" $(w,t)$, if any, on his list.
2. Each woman rejects all but the best acceptable offered contract.
3. Each man strikes any rejected offer from his list.
4. If any man was rejected at the last round, return to 1 (iterate).
5. Otherwise, the accepted contract offers are finalized.
```

There is also an extended woman-offering algorithm, with the obvious reversal of roles.

### Theorems

```{prf:theorem} Extended Matching Theorems
:label: extended-theorems
Let $\mu$ be the output of the extended man-offering algorithm. 
1. $\mu$ is a stable matching.
2. $\mu$ is the most preferred stable matching for each man.
3. $\mu$ is the least preferred stable matching for each woman.
4. The algorithm is “truthful” for men, but not for women.
```

### Examples and Intuition

Example: the matching may have $m$ and $w$ going to the concert $t$ at Bing tonight, which he prefers, rather than to the basketball game $t'$ at Maples, which she prefers, when both $t$ and $t'$ were acceptable to both.

Review of the results:

* Outcome is stable
* Man-best stable matching
* Woman-worst stable matching
* Truthful for men (not for women)

### Deferred Acceptance as an Auction?

Suppose the two sides are buyers and sellers.

* Each seller has one unit of its product and cares only about price and breaks ties in favor of the lowest numbered buyer.  
* Each buyer cares about the item and the price, breaking ties in favor of the lowest numbered seller.
With just one seller/one item,
* the buyer offering deferred acceptance algorithm is an ascending (”English”) auction.
* the seller offering deferred acceptance algorithm is a descending (”Dutch”) auction
With multiple sellers, the auction is a less familiar one: a multi-product ascending (or descending) auction.
