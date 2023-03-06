# Auction Design and Applications

## Reserve Prices

Two bidders, with values $v_1$ and $v_2$. Each $v_i$ drawn from uniform distribution on $[0,100]$.

```{admonition} Question
Can the seller benefit from setting a “reserve” price, that is, a minimum price below which she won’t sell?
```

Seller sets reserve price $r$. Runs an ascending auction. Clock starts from $r$ and goes up, so rational bidders with low values may decline to bid.

Three cases:
1. Both bidder values below $r \implies$ no sale.
2. One value above $r$, one below $r \implies$ sale at $r$.
3. Both values above $r \implies$ selling price equals the lower of the two values.

Revenue:

Expected revenue (add up three cases and probabilities)


```{list-table}
:header-rows: 1

* - Event
  - Probability
  - $\mathbb{E}[\text{Revenue}|\text{Event}]$
* - $v_1, v_2 < r$
  - $\frac{r}{100} \times \frac{r}{100}$
  - $0$
* - $v_i < r < v_j$
  - $2\times\frac{r}{100}\times\left(1-\frac{r}{100}\right)$
  - $r$
* - $v_1, v_2 > r$
  - $\left(1-\frac{r}{100}\right)\times\left(1-\frac{r}{100}\right)$
  - $r+\frac{1}{3}\left(100-r\right)$
```

Expected revenue is a cubic function of $r$:

\begin{align*}
\mathbb{E}[\text{Revenue}|r]&=0+2\frac{r}{100}\left(1-\frac{r}{100}\right)+\left(1-\frac{r}{100}\right)^{2}\left(r+\frac{100-r}{3}\right)
\end{align*}

Set $\frac{d}{dr}\mathbb{E}[\text{Revenue}|r] = 0$. Two solutions. Maximum revenue is achieved at $r^{*}=50$.

```{figure} ../images/reserve-price1.png
:name: reserve-price1
:height: 400px
```

TODO: improve graphic (make lines connect)

```{figure} ../images/reserve-price2.png
:name: reserve-price2
:height: 400px

Effect of Reserve with $N=2,3$
```

TODO: what do the blue vertical/horizontal lines mean?


## Case Study: eBay

[TODO slide 10]

