# Auction Theory

## Single Item Auctions

A seller has a single item that she wants to sell. How can she identify the right buyer and price? Why use an auction instead of simply setting a price? The seller may not know what price to set, and guessing can lead to problems: too high, no sale; too low, excess demand. Potential buyers know their max prices but don't always reveal them (everyone loves a good deal!). If **acceptance** of any offer is **deferred** until all offers can be compared, then the mechanism is called an **auction** and leads to **competition** and **price discover**.

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

TODO: interactive Desmos graph!

```{prf:proposition}
The second-price auction is the _only_ auction for this setting that has these three properties:
1. Truthfulness: the auction is always truthful
2. efficiency: the highest bid always wins
3. losing bidders pay nothing
```

TODO proof

## Vickrey-Clark-Groves (VCG) Mechanisms
```{index} Vickrey-Clark-Groves (VCG) Mechanisms
```
