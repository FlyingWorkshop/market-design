# Sponsored Search Auctions

## Background

<a href="https://www.statista.com/statistics/266249/advertising-revenue-of-google/" rel="nofollow"><img src="https://www.statista.com/graphic/1/266249/advertising-revenue-of-google.jpg" alt="Statistic: Advertising revenue of Google from 2001 to 2021 (in billion U.S. dollars) | Statista" style="width: 100%; height: auto !important; max-width:1000px;-ms-interpolation-mode: bicubic;"/></a><br />Find more statistics at  <a href="https://www.statista.com" rel="nofollow">Statista</a>

## Sponsored Search Auctions

```{index} sponsored search auctions
```

Search advertising is a huge auction market. In 2021, Google ad revenue in 2021 was $209 billion.

```{epigraph}
“Most people don’t realize that all that money comes pennies at a time.”

-- Hal Varian, Google Chief Economist
```

Google auctions advertisement space on certain keywords in search queries. For example, local furniture stores may compete with one another for the top link on a search for "office desks." Why use auctions instead of just setting prices? There are tens of millions of keywords, so it's impractical to set so many prices. Demand and especially supply change frequently, and auctions retain some price-setting ability. Today, the theory and practice of these auctions is an application of the assignment market model!

## Keyword Auctions

```{index} keyword auctions
```

* Advertisers submit bids for keywords
  * Offer a payment _per click_.
  * Alternatives: per impression or per conversion.

* Separate auction for every query
  * Positions awarded in order of bid (more on this later).
  * Google uses "generalized second price" format.
  * Advertisers pay bid of the advertiser in the position below.

* Some important features
  * Value is created by getting a good match of ad to searcher.
  * Multiple positions, but advertisers submit only a single bid.

### Brief History

1990s: websites sell advertising space on a “per-eyeball” basis, with contracts negotiated by salespeople; similar to print or television.

Mid-1990s: Overture (GoTo) allows advertisers to bid for keywords, offering to pay per click. Yahoo! and others adopt this approach, charging advertisers their bids.

2000s: Google and Overture modify keyword auction to have advertisers pay minimum amount necessary to maintain their position (GSP).

Auction design becomes more sophisticated; auctions used to allocate advertising on many webpages, not just search.

## Assignment Model (Variation)

```{index} assignment model (variation)
```

There are $k = 1, \dots, K$ positions on the page and bidders $n = 1, \dots, N$. Position $k$ has "click rate" $x_k$ where $x_1 > x_2 > \dots > x_K$. Bidder $n$ has value $v_n$ per click: $v_1 > v_2 > \dots > v_N$. So, bidder $n$'s value for position $k$ is: $v_{nk} = v_nx_k$. If bidder $n$ buys $k$ and pays $p_k$ per click, it earns $(v_n - p_k) x_k$. An efficient (total-value maximizing) assignment gives position $1$ to bidder $1$, position $2$ to bidder $2$, etc.

### Questions

Two positions: receive $200$ and $100$ clicks per day. Bidders $1, 2, 3$ have per click values $10, 4, 2$.

```{list-table}
:header-rows: 1

* -
  - Top
  - Second
* - Bidder $1$
  - $2000$
  - $1000$
* - Bidder $2$
  - $800$
  - $400$
* - Bidder $3$
  - $400$
  - $200$
```

Find the effecient allocation and compute the total value it creates.

```{dropdown} Solution
Bidder $1$ gets the top position: value $200 \times 10 = 2000$. Bidder $2$ gets the second position $100 \times 4 = 400$, so the efficient allocation creates value $2400$.
```

Find the lowest market clearing price.

```{dropdown} Solution
* Bidder $3$ demands nothing, so $p_1 \geq 400$ and $p_2 \geq 200$.
* Bidder $2$ buys the second position, so $400 - p_2 \geq \max(0, 800 - p_1)$.
* Bidder $1$ buys the top position, so $2000 - p_1 \geq \max(0, 1000 -p_2)$ 

So, the Vickrey/lowest market clearing prices are $600$ and $200$ (graphing this on des)
```

Graph the set of market-clearing prices in terms of per click values.

```{dropdown} Solution
Bidder $3$ demands nothing: $p_1, p_2 \geq 2$
Bidder $2$ demands position $2$: $4 \geq p_2 \geq 2p_1 - 4$
* Prefers position $2$ to nothing: $100 \times (4 - p_{2}) \geq 0$
* Prefers position $2$ to $1$: $200 \times (4 - p_{1}) \leq 100 \times (4 - p_{2})$
Bidder $1$ demands position $1$: $2 p_1 \leq 10 - p_2$
* Prefers position $1$ to $2$: $200 \times (10 - p_1) \geq 100 \times (10 - p_2)$
* Prefers position $1$ to nothing: $200 \times (10 - p_1) \geq 0$
```

### Price Premium for More Clicks

```{prf:remark}
:label: price-premium
_Per click_ prices must be higher for better positions!
```

```{prf:proof}
At market clearing prices, bidder $k$ must buy position $k$ and so prefers position $k$ to position $k - 1$ and to nothing. Hence:

\begin{align*}
(v_k - p_k) x_k &\geq (v_{k} - p_{k -1}) x_{k-1} \\
v_k &\geq p_k
\end{align*}

We have assumed that $x_{k-1} > x_k > 0$, so
\begin{align*}
(v_k - p_k)x_{k-1} \geq (v_k - p_k)x_k \geq (v_k - p_{k-1}) x_{k-1}
\implies p_{k-1} \geq p_k
\end{align*}
```

## Algorithmic Min/Max Clearing Price Discovery

We assume more bidders than positions, so $N > K$.

```{prf:algorithm} _lowest_ clearing price discovery
:label: lowest-clearing-price
1. Set $p_k = v_{K + 1}$ so that bidder $K + 1$ won't buy that position.
2. For $k <K$, given $p_{k+1}$, set $p_k$ so that bidder $k + 1$ will be just indifferent between buying position $k+1$ and $k$:
\begin{align*}
    (v_{k+1} - p_k)x_k = (v_{k+1} - p_{k+1})x_{k+1}
    \therefore p_k = v_{k+1} + (v_{k+1} - p_{k+1}) \frac{x_{k+1}}{x_k}
\end{align*}
```

```{prf:algorithm} __highest_ clearing price discovery
:label: highest-clearing-price
1. Set $p_k = v_{K}$ so that bidder $K$ is just willing to buy.
2. For $k <K$, given $p_{k+1}$, set $p_k$ so that bidder $k + 1$ will be just indifferent between buying position $k+1$ and $k$:
\begin{align*}
    (v_{k} - p_k)x_k = (v_{k} - p_{k+1})x_{k+1}
    \therefore p_k = v_{k} + (v_{k} - p_{k+1}) \frac{x_{k+1}}{x_k}
\end{align*}
```

## Pay-As-Bid Auctions

```{index} pay-as-bid auctions
```

Pay-as-bid auctions are sometimes also called overture auctions.

```{prf:algorithm} Pay-As-Bid Auctions
:label: pay-as-bid
1. Each bidder submits a single bid (in dollars per click)
2. Top bid gest position $1$, second position $2$, etc.
3. Bidders pay their bid for each click they get.
```

Pay-as-bid auctions are sometimes also called overture auctions.

```{prf:remark}
The pay-as-bid auction is unstable.
```

```{prf:proof}
Consider as before two positions that receive $200$ and $100$ clicker per day. Bidders $1,2,3$ have per-click values $10, 4, 2.$
Then running the pay-as-bid auction yields:
* Bidder $3$ will offer up to $2$ per click
* Bidder $2$ must bid $2.01$ to get second slot
* Bidder $1$ wants to bid $2.02$ to get top slot.

But then bidder $2$ wants to top this, and so on.
```

We also observe this instability in practice.

```{figure} ../images/sawtooth-bidding.png
:name: sawtooth-bidding
:height: 600px

A "sawtooth" pattern caused by auto-bidding programs. {cite:p}`sawtooth`
```

## Google Generalized Second Price (GSP) Auctions

```{index} generalized second price auctions
```

```{index} GSP auctions
```

```{prf:algorithm} Generalized Second Price Auctions
:label: GSP
1. Bidders submit bids (in dollars per click)
2. Top bid gets slot $1$, second bid gets slot $2$, etc.
3. Each bidder pays the bid of the bidder below them.
```

Intuitively, this seems more stable than pay-as-bid auctions, but do the bidders want to bid truthfully?

```{prf:theorem}
GSP auctions aren't truthful.
```

```{prf:proof}
Consider two positions with $200$ and $100$ clicks. Also consider a bidder with value $v_1 = 10$. There are competing bids $v_2 = 4$ and $v_3 = 8$. If our bidder bids $10$, they get the top position and pay $8$ and profit $200 \times 2 = 400$. However, if they bid below their value at $5$, then they win the second position and pay $4$, so their profit is $100 \times 6 = 600$. So, bidding untruthfully is more profitable.  
```

Note that the GSP isn't always untruthful. If the competing bids were instead $6$ and $8$, then the dominant action for the bidder would have been to bid truthfully at $10$.

```{seealso}
Get more practice [here](https://colab.research.google.com/drive/1Io1l9eAxCRpfQL7pa2i8s5anwWKOvcYR?usp=sharing)!
```

### Finding GSP Equilibria

Fix any set of market clearing per-click prices: $p_1, \dots, p_N$. Assume that $N > K$.
There is a GSP equilibrium in which:
1. Bidder 1 bids any amount more than $p_1$
2. Bidder 2 bids $p_1$
3. Bidder 3 bids $p_2$.
4. etc.
Bidder $k$ will prefer to buy position $k$ and pay $p_k$ rather than buy position $m$ and paying $p_m$ – that’s why the prices were market clearing!

## Vickrey Auction

```{index} Vickrey auction
```

```{prf:algorithm} Vickrey auction
:label: vic-auc

1. Bidders submit bids (dollar per-click)
2. Seller selects the assignment that maximizes total value
  * Puts highest bidder in top position, next in 2nd slot, etc.
3. Charges any winner the total value that its bid displaces.
  * For bidder $n$, each bidder below $n$ is displaced by one position, so must add up the value of all these “lost” clicks.   
```

Dominant strategy to bid one’s true value. Facebook uses a Vickrey auction.

### Pricing

Order per-click bids: $b_1 > b_2 > \dots > b_K$

Consider bidder who wins $k$th slot.
* Displaces $k+1, \dots, K$
* Leaves $1, \dots, k - 1$ intact.
Displaced bidder $j$ would get $x_{j-1}$ clicks in position $j-1$, but instead gets $x_j$ clicks in position $j$. 
$k$’s Vickrey price is $\sum_{j > k} b_j(x_{j-1} - x_j)$.

```{image} ../images/vickrey-pricing.png
:width: 200px
:align: center
```

```{note}
In GSP, bidder $k$ pays: $b_{k+1}x_k$
```

## The Vickrey (VCG) Formula

In the Vickrey, if a bidder wins, then it pays the resulting “opportunity cost.”  
* Payment = the loss of value to others caused by the change. 
* Consequence: A bidder prefers the efficient allocation.  

The VCG “pivot” mechanism extends and generalizes that idea.
* The problem is to choose some decision $x \in X$ from a finite set.
* Each participant $n$ reports a value function $v_n: X \to \mathbb{R}_+$
* Mechanism selects $x^*$ to solve $\max_{x \in X}\sum_n v_n(x)$.
* Without $j$, the mechanism would select $x_j^∗$ to $\max_{x \in X}\sum_{n \neq j} v_n(x)$.
* VCG pivot mechanism: $j$ pays $\sum_{n \neq j}(v_n(x_j^*) - v_n(x^*))$
  * That is, $j$ pays for any loss she causes to others, so she prefers to cause a loss only when her own benefit is larger!

## Summary of Results

**Result 1.** The generalized second price auction (GSP) does not have a dominant strategy.

**Result 2.** The Nash Equilibria of the GSP are “equivalent” to the set of competitive equilibria[^footnote1]:
Bidders obtain their surplus-maximizing positions
For any NE of the GSP, the prices paid correspond to market clearing prices, and for any set of market clearing prices, there is a corresponding NE of GSP.

**Result 3.** The Vickrey auction is truthful and its payments in the position auction are equal to the lowest market-clearing prices. 

## Keyword Auction Design

Platforms can exercise some control over prices
* Restricting the number of slots can increase prices.
* Setting a reserve price can increase prices

Platforms can also “quality-adjust” bids
* In practice, ads that are more “clickable” get promoted.
* Bids can be ranked according to bid * quality.
* This gives an advantage to high-quality advertisements.

## Sponsored vs Organic Results

Google and Bing show “organic” search results on the left side of the page and “sponsored” results above or on the right.

The assignment of positions on the page is different
* Organic search results: use algorithm to assess “relevance”
* Sponsored search results: use bids to assess “value”

To some extent there is competition: if a site gets a good organic position, should it pay for another? Search engines have to think about maximizing user experience but also about capturing revenue from advertisers.

## Summary

* Search auctions create a real-time market in which advertising opportunities are allocated to bidders. 
* Auction theory suggests that the “generalized second-price” rules used in practice might be reasonably efficient.
  * GSP is not “truthful” but it has efficient Nash equilibria with competitive prices.
  * Vickrey auction is truthful but more complicated.
* In practice, the search platforms have some scope to engage in optimal auction design. 


[^footnote1]: Small caveat here, there are also some “dominated” NE of the GSP that we're ignoring.
