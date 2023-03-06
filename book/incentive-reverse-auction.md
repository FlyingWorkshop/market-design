# Incentive Reverse Auction

## What is the Broadcast Incentive Auction?

```{tip}
Watch a [video](https://www.youtube.com/watch?v=7k450BJbcMY)!
```

### Constrained Channel Assignments

```{image} ../images/constrained-channels.png
:height: 300px
:align: center
:name: constrained-channels
```

For each station, fewer than $0.5\%$ of existing customers may suffer interference from another station.

```{image} ../images/one-station-interference.png
:height: 300px
:align: center
:name: one-station-interference
```

Each “node” represents the location of a (ultra high frequency) UHF-TV station. Each “arc” represents a pair of stations that cannot both be assigned to the same channel without causing unacceptable interference. Nodes connected to the central red node are shown in pink.

```{image} ../images/node-map.png
:height: 300px
:align: center
:name: node-map
```

A set of stations can all continue to broadcast if there is a way to assign channels to the stations without interference. There are about $130,000$ co-channel constraints shown in the graph. ($2.7$ million detailed constraints). This is similar to graph coloring, which is an [NP-complete problem](https://en.wikipedia.org/wiki/NP-completeness). 

## FCC's 2011 Initial Internal Proposal

They proposed a variant of the pivot mechanism (“Vickrey auction”) with allocation and prices:

\begin{align*}
S^{*} &= \arg\max_{S \in F}\sum_{j \in S}v_j\\
p_i &= \sum_{j \in S^{*}} v_j - \max_{S \in F, i \in S} \sum_{j \in S - \{ i \}} v_j
\end{align*}

where $S^{*}$ is the set of stations to remain on-air and $p_i$ is the price paid to stations going off-air $(i \not\in S^{*})$ which can be interpreted as the "opportunity cost."

TODO: don't understand the pricing error

Percentage pricing errors around $2500$ times optimization errors. 
FCC computational experiments showed that computed approximate Vickrey prices were badly inaccurate

### Problems with Vickrey Auction

1. Depends on intractable computations 
2. Requires very high trust
3. Ignores procurement budgets
4. Is not group strategy-proof
5. Cannot balance efficiency and cost objectives
6. May produce an uncompetitively high price vector  
7. Reveals winning bidders’ values

```{important}
As we will see, these deficiencies can _all_ be overcome at little efficiency cost for the incentive auction!
```

Vickrey auctions also require _too much trust_ in practice. The auction model can be difficult to interpret, so many bidders barely understand the computations. Most cannot determine the outcomes from the bids. The FCC can't even guarentee that computations will be accurate, and by law, they can't share bid data to allow verifying the computation.

TODO: is it because the model is super big?

```{prf:remark}
The Vickrey auction is not budge aware, group strategy-proof, or generally price competitive.
```

```{image} ../images/incentive-example.png
:height: 150px
:align: center
:name: incentive-example
```
```{prf:proof}
Consider the following example.
Initially, stations $A$ and $B$ share a channel and $C$ uses another. Our goal is to reduce use from two channels to one. Optimization: If $v_A + v_B < v_C$, then we should buy $A$ and $B$; otherwise, we should buy $C$. If $C$ wins, the Vickrey prices are $p_C = v_A + v_B$. If $A$ and $B$ win, they are $p_A = v_C - v_B$ and $p_B = v_C - v_A$. As this example shows, the Vickrey auction is:
* NOT budget aware: infeasible if total price exceeds budget  
* NOT group strategy-proof: if $A$ and $B$ both bid $0$, they will win and receive maximum Vickrey payments of $\hat{p}_A = \hat{p}_B = v_C$
* NOT generally price competitive. If $A$ and $B$ win, $p_A + p_B > v_C$
```

### Milgram-Segal Descending Clock Auctions

```{index} Milgrom-Segal auctions
```

Milgrom-Segal descending clock auctions overcome the problems of the Vickrey auction:
1. can compute well and quickly  
2. require no bidder trust  
3. can accommodate budget constraints
4. are group strategy-proof (without side payments)
5. can accommodate any mix of efficiency and cost minimization objectives 
6. produce competitive, market-clearing prices
7. preserve winner privacy

## Clock Auctions as Heuristics for Optimization

### The Channel Reallocation Optimization Problem

Goal: Given the current set of stations $N$, find the feasible subset of stations $S^{*}$ that should continue to broadcast (in a more limited set of channels) to maximize the total value of the stations remaining on-air. 

\begin{align*}
\max_{S \in F} \sum_{n \in S} v_n
\end{align*}

where $v_n$ are station values.

TODO: what does "feasible to pack mean?" slide 14

### The Classic “Knapsack Problem”

\begin{align*}
\max_{S \subseteq N} \sum_{n \in S} v_n \text{ subject to } \sum_{n \in S} s_n \leq K
\end{align*}
where $K$ is the knapsack constraint.

```{index} greedy packing
```

```{prf:algorithm} Greedy Packing
:label: greedy-packing

1. Order items so that $\frac{v_1}{s_1} > \frac{v_2}{s_2} > \dots$ and ignore ties. 
2. “Pack” items in numerical order so long as there is space remaining. If there is no room to pack an item, set it aside and continue.
```

The difference between the maximum value and the greedy algorithm value is at most $\frac{v_{m}}{s_{m}}\left(K-\sum_{j=1}^{m-1}s_{j}\right)$: a fraction of the value of the first item 𝑚 that is excluded from the knapsack. 

[TODO continue from slide 16]