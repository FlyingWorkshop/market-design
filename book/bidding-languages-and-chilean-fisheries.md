# Bidding Languages + Chilean Fisheries

## Bidding Languages

### So Many Numbers to Report!

* With $K$ different items for sale, a value report for the Shapley-Shubik assignment mechanism uses $K$ numbers per bidder–one for each item. 
    * In that case, individual items are _substitutes_: if one item is most preferred at prices $p$ by a bidder, it is still most preferred if the other item prices increase. 
    * Deferred acceptance depends on this substitutes property! 
* If a bidder may have any value for any non-empty subset, then since there are $2^K$ subsets, there are $2^{K-1}$ numbers to report. 
* If there are $n_k$ items of types $k = 1, \dots, K$, then a package is an element of $\{0, \dots, n_1\} \times \dots \times \{0, \dots, n_k\}$, so the number of non-empty packages is $(n+1) \times \dots \times (n_k + 1) - 1$.

```{glossary}
substitutes
    Formulation: 
    * Goods of types $1, \dots, K$. $X = \{0, \dots, n_1\} \times \dots \times \{0, \dots, n_k\}$.
    * Demand function $d: \mathbb{R}_+^K \to X$ maps prices to quantity vectors.

    Goods are substitutes if for all $k$ and price vectors $p,p' \in \mathbb{R}_+^K$ with the properties that $p \geq p'$ and $p'_k = p_k$, $d_k(p) \geq d_k(p')$. 

    In words, “raising the prices of other goods never reduces demand for good $k$.” 

complements
    TODO
```

Complements example:
* The two kinds of goods are left and right shoes. Raising the price of left shoes reduces buyers’ demand for right shoes.

Substitutes examples
* 0-1 or 1-1 substitution
    * Location, quality, date, contract terms 
    * Fonterra & milk powder
    * PG&E and energy sources 
    * Haircuts
* Other rates of substitution  
    * Fishing boat capacity




TODO: what are 0-1, 1-1 substitution? How are haircuts? how are fishing boats?



