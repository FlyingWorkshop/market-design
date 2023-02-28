# Auction Theory

## Single Item Auctions

A seller has a single item that she wants to sell. How can she identify the right buyer and price? Why use an auction instead of s1. ply setting a price? The seller may not know what price to set, and guessing can lead to problems: too high, no sale; too low, excess demand. Potential buyers know their max prices but don't always reveal them (everyone loves a good deal!). If **acceptance** of any offer is **deferred** until all offers can be compared, then the mechanism is called an **auction** and leads to **competition** and **price discover**.

```{epigraph}
Auctions are games that guide prices to mimic markets.
-- Josh Gross
```

We can model this with $N$ bidders. The item is worht $v_n > 0$ to bidder $n$ (if $v_n \leq 0$ then they don't join the auction). Losing bidders have payoffs of zero. The winning bidder pays $p$ has payoff $v_n - p$.


## Sealed-Bid Auctions
```{index} sealed-bid auctions
```

A sealed bid auctions (also called "blind auctions") are auctions where bidders submit bids secretly and simultaneously, so no one knows the bid of anyone else. The highest bid always wins, but they don't always pay the highest price for reasons we'll explore later.

```{glossary}
"First-Price" Auctions
    * Each bidder privately writes down a number
    * The highest number wins (ties broken arbitrarily)
    * The winning bidders pays a price equal to **her bid**
    * *Each bidder should bid **less than the maximum** they're willing to pay*

"Second-Price" Auctions
    * Each bidder privately writes down a number
    * The highest number is the winning bid (ties broken arbitrarily)
    * The winning bidder pays a price equal to the highest losing bid
    * Second-price auctions are truthful: each bidder should bid exactly the maximum it is willing to pay

universal best reply
    The action $\bar{a}_n$ is a _universal best reply_ for player $n$ if for _all_ $a_{-n} \in A_n$, we have $\bar{a}_n \in \text{argmax}_{s_n} u_n(a_n, a_{-n})$
````

```{prf:remark}
:label: dom-strat
The strategy $\bar{a}_n$ is a **dominant strategy** if it's the unique universal best reply.
```

## Truthful Mechanisms


```{glossary}
truthful (auction)
    An auction is **truthful** if each player $n$ has a universal best reply, which is to report its true value $v_n$ to the auctioneer.
```

```{prf:proposition}
The second-price auction is truthful.
```

```{prf:proposition}
The second-price auction is the _only_ auction for this setting that has these three properties:
1. Truthfulness: the auction is always truthful
2. efficiency: the highest bid always wins
3. losing bidders pay nothing
```
We provide a sketch of the prooof. The details are left as an excercise.
```{prf:proof}
1. Truthful incentives $\Rightarrow$ given others' bid, all of $n$'s winning bids must always lead to the same price $p(v_{-n})$.
2. Truthful incentives + Losers pay zero $\Rightarrow$ $n$ wins when its reported value exceeds $p(v_{-n})$.
3. Efficiency $\Rightarrow$ $n$ wins when its reported value exceeds the highest opposing value $\max_{m\neq n}v_m$.
4. $(2)$ and $(3) \Rightarrow p(v_{-n}) = \max_{m\neq n}v_m$.
```

## Vickrey-Clark-Groves (VCG) Mechanisms
```{index} Vickrey-Clark-Groves (VCG) Mechanisms
```

Consider an abstract setting in which our “system” must choose one from a finite set of outcomes.
Examples:
* How many items to assign to each bidder (from a set of identical items)?
* Who wins which from a set of distinct items? 
* Which room in a rental house should be assigned to each roommate?
* Whether to build a children’s playground at the apartment complex and how to equip it?  
* Building a bridge: whether to do it, where and which kind?

The people are $n=1,\dots,N$ and the possible decisions are numbered $k=1,\dots,K$. Person $n$ has value $v_{nk}$ for decision $k$. Notation: $v_n=(v_{n1},\dots,v_{nK})$, $v=(v_1,\dots,v_N)$. The system collects value reports and uses those to select a value-maximizing decision $k^{*}$: $k^* \in \arg\max_k v_{1k}+\dots+v_{Nk}$. But agents could misreport their values. Is there any way to incentivize truthful value reports? How?

Some Ideas:
* A “direct mechanism” asks each player to report values for each possible decision. 
* The system then uses the reports to choose the decision $k^*$ that maximizes the total welfare and makes a payment (positive or negative) to each player.
* So… each player can, by exaggerating her report, cause the system to select any decision. Why would she report truthfully? 
* Solution: arrange the payments to players to align each player’s interest with the total welfare.  
* Given any reports by others, any two reports by a single agent $n$ that lead to the same decision $k$ must lead her to receive the same payment, which we denote by $p_n(k,v_{(-n)})$.

```{prf:algorithm} Vickrey-Clark-Groves (VCG) Mechanism
:label: vcg-mechanism
1. Each player $n$ reports values $v_n\in\mathbb{R}^K$
2. The system uses reported values to select $k^(v):\ k^*(v)\in\arg\max_{k}\sum_{j=1}^N v_{jk}$
3. If $k^*(v)=k$, we pay player $n$:
\begin{align*}
p_n(k,v_{-n})&=\sum_{j\neq n} v_{j,k} + f_n(v_{-n})
\end{align*}
4. Then $n$’s payoff is
\begin{align*}
$v_{nk}+p_n(k,v_{-n})=v_{nk}+\sum_{j\neq n} v_{jk} + f_n(v_{-n})$
\end{align*}
```

```{prf:theorem} VCG is Truthful
:label: vcg-truthful
Theorem
1. Every VCG mechanism is truthful and selects a decision in $k^*(v)$.
2. Every mechanism that is truthful and selects a decision in $k^*(v)$ is a VCG mechanism.
```

```{prf:proof}

(Part 1) We must show that $n$'s payoff from reporting $v_n$ truthfully minus her payoff from making any other report $\hat{v}n$ is always non-negative. Truthful reporting leads to an outcome $k\in k^*(v_n,v{-n})$. Any other report of $\hat{v}_n$ leads to an outcome $\hat{k}\in k^*(\hat{v}_n,v_{-n})$, so the payoff difference is:

\begin{align*}
& (\left(v_{nk}+p_{n}\left(k,\ v_{-n}\right)\right)-\left(v_{n\hat{k}}+p_{n}\left(\hat{k},v_{-n}\right)\right) \\
&=\left(v_{nk}+\sum_{j \neq n}^{ }v_{jk}+f_{n}\left(v_{-n}\right)\right)-\left(v_{n\hat{k}}+\sum_{j \neq n}^{ }v_{j\hat{k}}+f\left(v_{-n} \right)\right) \\
&\ge0
\end{align*}

The $f_n(v_{-n})$ terms cancel one another. The remaining difference is non-negative because $k\in k^*(v_n,v_{-n})$ maximizes total welfare.

(Part 2) By construction, for any non-VCG payment rule, there is some ${v_{-n}}$ such that participant $n$’s total payoff ${v_{nk}+p_n(k,v_{-n})}$ is misaligned with the total welfare, say by favoring some $\hat{k}$ over ${k'}$ by a positive amount ${2\delta>0}$.

When ${v_n}$ is such that, given ${v_{-n}}$, the total welfare is ${\delta}$ higher for ${k'}$ than $\hat{k}$, $n$ will still favor outcome ${\hat{k}}$ and its associated payment by ${\delta}$. By reporting a ${\hat{v}_n}$ according to which $\hat{k}$ is uniquely valuable, $n$ can manipulate the mechanism to select outcome ${\hat{k}}$, which she favors: truthful reporting fails to maximize $n$’s payoff.

TODO: finish proof (slide 28 lecture 9)
```

## Revenues

(20 more slides)