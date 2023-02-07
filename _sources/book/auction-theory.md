# Auction Theory

## Single Item Auctions

A seller has a single item that she wants to sell. How can she identify the right buyer and price? Why use an auction instead of simply setting a price? The seller may not know what price to set, and guessing can lead to problems: too high, no sale; too low, excess demand. Potential buyers know their max prices but don't always reveal them (everyone loves a good deal!). If **acceptance** of any offer is **deferred** until all offers can be compared, then the mechanism is called an **auction** and leads to **competition** and **price discover**.

```{epigraph}
Auctions are games that guide prices to mimic markets.
-- Josh Gross
```

## Sealed-Bid Auctions

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
````