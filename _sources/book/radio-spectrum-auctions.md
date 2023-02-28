# Radio Spectrum Auctions

```{image} ../images/2003-freq-alloc.png
:align: center
```

## FCC Spectrum Auctions

Federal government assigns rights to use the radio spectrum for television, radio, cell phones, etc. – historically done by administrative process or lottery.

Auctions to assign radio spectrum licenses
Suggested by Herzel (1951) and Coase (1959) – paper is most famous for a footnote in which he suggested the Coase Theorem!
FCC switched to auctions in early 1990s, adopting the Milgrom-Wilson auction proposal. Other countries adopted essentially the US design, sometimes with modifications. 

Spectrum auctions have fostered a great deal of interest in auctions and auction design – a difficult problem, with high stakes for consumers, firm and governments.

### Resolving Radio Spectrum Interference

>  What this analysis demonstrates, so far as the radio industry is con is that there is no analytical difference between the problem of interf tween operators on a single frequency and that of interference betw tors on adjacent frequencies. The latter problem, like the former, can  by delimiting the rights of operators to transmit signals which inte might potentially interfere, with those of others. Once this is done, left to market transactions to bring an optimum utilization rights.

> It is, of course, true that the distribution of wealth as between the doctor a fectioner was affected by the decision, which is why questions of equity bulk s such cases. Indeed, if the efficiency with which the economic system worked was  independent of the legal position, this would be all that mattered. But this is  of all, the law may be such as to make certain desirable market transactions This is, indeed, my chief criticism of the present American law of radio comm Second, it may impose costly and time-consuming procedures. Third, the legal  of rights provides the starting point for the rearrangement of rights through ma actions. Such transactions are not costless, with a result that the initial deli rights may be maintained even though some other would be more efficient. Or, original position is modified, the most efficient delimitation of rights may not. Finally, a waste of resources may occur when the criteria used by the court rights result in resources being employed solely to establish a claim.

{cite}`coase`

## Simultaneous Ascending Auction (SAA)
```{index} simultaneous ascending auctions
```

```{prf:algorithm} Simultaneous Ascending Auction
:label: saa
Auction is run in a potentially long series of rounds. 
Each round begins with standing high bid on each license (initially the seller), and a minimum bid increment.
Each bidder can submit bids on any number of items, subject to an eligibility and activity rule.
If no bids on a license, standing high bidder remains. If multiple bids, one bid selected to be the new high bid.
Information about bids is revealed; move to next round.
Auction ends when no new bids are submitted. 
```

### Motivation

Why simultaneous? .. relative to sequential auctions
Price discovery! Bidders get some information about the prices of all licenses before finalizing their bids for all.  
This leads to more efficient package choices and equalization of prices for similar items.  

Why ascending? … relative to sealed bidding. 
Price discovery! Sealed bids convey too little information, requiring guesswork. Winning bidders “preserve privacy” about their values...
But... there may be more opportunity for demand reduction, collusion.

### Termination Rule

The FCC ends the auction for all items only when there is no new bid for any item. 

Prevents “sniping”, in which last second bidders steal some item from the previous highest bidder. 

### Activity Rules

Activity rule are used to keep the auction moving
Each license assigned some number of points
Bidders start with eligibility points, must use them each round or else have their eligibility reduced.
Necessary so bidders don’t just sit back and wait.

In practice, though, it can complicate bidding
Suppose NY is 200 points; LA and SF are each 100.
Easy to switch to SF/LA if outbid on NY, but what if you are bidding for SF/LA and are outbid on LA only?
A consequence: bidding on large licenses stops earlier. 

#### Example

[TODO slide 14]


### Theory

```{glossary}
    straightforward bidding
        Bidding is “straightforward” if each round bidders bid for the set of licenses that offer the most profit at current prices.
```

```{prf:theorem}
If bidders have “substitutes” values (e.g. want only one license) and bid straightforwardly, the SAA leads to an efficient allocation and lowest competitive prices.
```

Magic of the Market Results
Auction outcome is “as if” the seller knew all the values and used a computer to find the efficient allocation & market-clearing prices – auction discovers the right prices and quantities.
Bidders have “no regret” – at the final prices, each winner gets exactly the licenses that gives it the most profit, and no loser would like to be a winner (assignment is “stable” given prices).

## "Gaming" in Spectrum Auctions

### Entry Deterance

[TODO slide 22]



