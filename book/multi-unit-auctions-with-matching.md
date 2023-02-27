# Multi-Unit Auctions with Matching

Some auctions involve sale of different types of items. Spectrum licenses in different regions, seats for a concert or event, advertising spots on the internet, assets of a company being liquidated, pieces of a procurement contract.

## Connection to Gale-Shapley “Marriage Problem”

Assignment models seeks to allocate items to people with different preferences, with each person getting $\leq 1$ item. This sounds like a matching problem. Before we tried to assign the items without payments.
Now, we assume items can have money prices.

Certain auctions function similarly to matching algorithms–they implicitly include _deferred acceptance mechanisms_ to find efficient allocations, ideally also providing truthful (or “near-truthful”) incentives.

## Assignment Model

Sets of individuals $\{1,\ldots,N\}$ and items $\{1,\ldots,𝐾,\emptyset \}.$ An assignment $k$ maps individuals to items, so $k(i)$ is the item assigned to individual $i$ and $k(i) = \emptyset$ means that no item is assigned to $i$.

Payoffs: Let $v_{ik}$ denote individual $i$’s value for item $k$. If $i$ gets item $k$ and pays $p_k$, her utility is $v_{ik} - p_k$.

Connection to the “marriage problem”: If prices were fixed, then each buyer would rank alternatives in order according to $v_{ik} - p_k$ and Gale-Shapley could be applied. But our seller’s rank according to prices only, so we won’t hold those fixed. 


## Aside: Matching with Contracts?

We have already discussed a closely related model in our study of matching with contracts, in which parties cared about a match and terms.
“Terms” can include money amounts. In that theory, we assumed “strict preferences”–so, no ties. In economics, it is common to model money by a continuous variable, and this can make ties unavoidable. That changes some details of the analysis, but the main thrust is very similar. 
Additional connections will be made on later slides.

### Example: Cubicle Assignment

Say we are tasked with assigning cubicles to economics graduate students. To find an effecient assignment without prices or money, we can assign random numbers (RSD). The assignment is Pareto efficient for any random order, so there are many Pareto efficient assignments! Adding money changes things.

#### Questions
Suppose that students can trade offices for money.
1. Is the outcome of an office draw Pareto efficient? 
2. What does a Pareto efficient outcome look like? 
3. What algorithm might identify an efficient allocation?

## Pareto Efficiency

```{glossary}
Pareto domination
    An assignment is _Pareto dominated_ if there is another assignment and set of cash payments that results in everyone being better off. 

Pareto efficient (auctions)
    An assignment is Pareto efficient if it is not Pareto dominated.

The total value (or surplus) of the assignment $k$ (that assigns to each $i$ the item $k(i)$) is $v_{1k(1)} + \dots + v_{Nk(N)}$.
```

```{admonition} Question
What’s the relationship between Pareto efficiency & total value?
```

### Example

We have three people $a$, $b$, and $c$ and two items $x$ and $y$. The value matrix is:

$$
\begin{bmatrix}
30 & 60 \\
20 & 40 \\
10 & 20 
\end{bmatrix}
$$

The rows from top to bottom represent the values for $a$, $b$, and $c$. The left and right columns represent $x$ and $y$ respectively.

1. Can it be efficient to assign $\{(a, x), (b, y), (c, \emptyset)\}$ with some payments, so $b$ gets his most preferred item?
2. Identify a Pareto efficient allocation.

```{dropdown} Solution
TODO: check this with Paul
1. Yes. 
2. TODO
```

## Efficient Assignments
````{prf:theorem} Efficient Assignments
:label: efficient-assignments
When payoffs are value plus cash and total transfers must be equal to zero, an assignment with transfers is Pareto efficient if and only if no other assignment has a higher total value.
````
```{prf:proof}
Suppose an assignment achieves the maximum total value. Then any change in the assignment and any payments reduce the total value of all participants, so *someone* must lose from this change. Hence, such an assignment is Pareto efficient. 

Conversely, suppose an assignment does NOT maximize the total value. Then there is another assignment of items that adds some amount $\Delta > 0$ to the total value. Then, it is feasible to switch to this alternate assignment, make transfers so that everyone is indifferent about the change, and make additional payments to everyone of $\Delta / N$. All strictly prefer that arrangement, so the original assignment is not efficient. 
```

## Algorithm to Allocate Efficiently?

Suppose items are initially owned by a seller that has zero value for the items, and suppose the seller wants to allocate the items efficiently. A seller might also care about selling for high prices, but we won’t focus on that concern today. Let’s consider an auction mechanism in which prices rise until all offers are accepted: a kind of **deferred acceptance mechanism.**

## Ascending (Clock) Auction

```{prf:algorithm} Ascending Auction
:label: ascending-auction
Seller has a price clock for each item.
1. Price of each item starts at $0$.
2. Buyers demand their most preferred (acceptable) item-price combination.
3. If any good has "excess demand" (i.e., more than one bids), increase its price "slightly" and return to step $1$. Otherwise, end.
```
Assumptions:
* At any given moment, each buyer bids for the item it wants most at the current clock prices (“truthful bidding”).
* Prices rise continuously rather than “jumping” discretely.

### Example 1
Three bidders $a, b$ and $c$. Two items $x$ and $y$.

$ \begin{bmatrix}
30 & 60 \\
20 & 40 \\
10 & 20 
\end{bmatrix}  $

What is the efficient assignment?
```{dropdown} Solution
$\{(a, y), (b, x)\}$
```

### Example 2

TODO

### Example 3: Market-Clearing Prices

TODO

ADD PARALLELOLPIPED with PLOTLY


## The Magic of the Market

TODO