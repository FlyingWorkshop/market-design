# Housing Allocation

In some matching markets, only one side of the market has preferences (or we care mostly about the preferences of one side). Sample applications include students picking housing on campus, organ transplants, school choice, and professional sports teams drafting college athletes.

## House Allocation Problem
$N$ individuals and $N$ houses (generalizable to $\neq$). Each individual has strict preference over houses.
The goal is to assign each individual to a house.

Pareto Efficient
: An allocation is Pareto efficient if no pair of individuals, or set of individuals, can “all do better” by trading houses.

```{admonition} Intuition
Participation in the mechanism is voluntary and groups of students can swap rooms/houses among themselves.
```

Stability
: An outcome is unstable if a coalition of agents _blocks_ a candidate assignment: i.e., from their initial endowments, there is another assignment they can arrange for themselves that they all prefer.  

Core
: The _core_ is the set of feasible unblocked assignments. 

Core assignments are Pareto efficient. Inefficient assignment would be blocked by the “coalition of the whole.” Not all Pareto efficient assignments are in the core: the core imposes additional constraints that respect prior ownership.

## (Random) Serial Dictatorship

```{prf:algorithm}
1. Each student gets a priority (perhaps randomly assigned as in the housing draw).
2. Students pick houses in order of their priority.
```

### Truthful and Efficient
```{prf:theorem}
The serial dictatorship mechanism is efficient (i.e., no mutually agreeable trades afterwards) and truthful (no incentive to misreport). 
```
```{prf:proof}
(Truthful)
The individual with first pick gets her preferred house, so clearly has no incentive to lie.
The individual with second pick gets her preferred house among remaining houses, so again has no reason to lie.
And so on $\ldots$

(Effecient)
The individual with priority one would do worse after any change in her house.
Given that the individual with priority #1 is not changing, the individual with priority #2 would do worse by any change.
And so on $\ldots$
```

#### Example

There are three people $1, 2, 3$ and three houses $A, B, C$.
Individual preferences:
* $1: A \succ B \succ C$
* $2: A \succ C \succ B$
* $3: B \succ C \succ A$

What is the outcome if the order of picking is $1, 2, 3$? Is this outcome Pareto efficient?

```{dropdown} Solution
The assignment is $\{(1, A), (2, C), (3, B)\}$. The matching is Pareto effecient.
```

## Top Trading Cycles
Now imagine that individuals start by owning a house, but the original allocation might be inefficient.
```{prf:algorithm} Gale's TTC Algorithm
1. Each house points to its owner
2. Each person points to her most preferred (remaining) house
3. This creates a directed graph; houses and people are “nodes.” 
    * There is at least one cycle. (Why?)
    * Each person is in at most one cycle. (Why?)
4. Remove all cycles, assigning people to the house to which they are pointing.
5. End if no houses or people remain. Otherwise, return to step 1.
```

### An Important Variation
What if we changed the algorithm, replacing “remove all cycles” with “remove one cycle”? 
```{prf:proposition}
The order of elimination of cycles does not affect the TTC outcome. 
```
Proof of this proposition (by mathematical induction, delaying the elimination of any particular cycle for $n$ rounds) is left as an exercise.

### Uniqueness

```{prf:theorem}
The outcome of the TTC algorithm is the unique core assignment in the housing market.
```

This is an amazing theorem. It asserts that: (1) a core assignment exists, (2) it's unique, and (3) it can be found by the TCC algorithm.

```{prf:proof}
The outcome of TTC is a core assignment:
No blocking coalition can improve any agent matched at round one (because all such agents get their first choices).
No blocking coalition can improve any agent matched in first two rounds (because, without changing assignments of the round 1 agents, the round two agents are already getting their best remaining houses). 
And so on by mathematical induction.

Uniqueness: 
Consider any proposed assignment $x$ that reassigns some round one individual from her TTC house. Then the round one group is a blocking coalition: it can give all its members their most preferred houses. 
Inductively, consider any assignment $x$ that does not reassign any individual from TTC rounds $1,\ldots,k$ but does reassign someone from round $k+1$. Then the round $k+1$ group blocks $x$, because it gives all its members their most preferred remaining houses. 
Hence, by mathematical induction, any assignment $x$ other than the TTC assignment is blocked. ∎
```

### Truthful

```{prf:theorem}
The TTC algorithm is truthful.
```
```{prf:proof}
Proof. Consider agent $n$ and fix the reports of all other agents. If we run the TTC algorithm, eliminating only cycles not involving agent $n$ until no more such cycles remain, then agent $n$’s highest ranked remaining house will be assigned to $n$ at the next round. With that order of elimination of cycles, agent $n$ can do no better than to report her ranking of houses truthfully.
By our earlier Proposition, the TTC assignment is independent of the order of elimination of cycles. ∎
```

```{attention}
Get more practice [here](https://colab.research.google.com/drive/1XLvZAQjAziBjRF3UPDKXkOnIBYN4CW8O?usp=sharing)!
```

## RSD with Incumbents

What can we do if some people start with houses (“incumbents”) but others do not?

A common problem in allocating student housing
Many universities, e.g. Michigan, Duke, Northwestern, Penn, CMU, use a variation of random serial dictatorship (with incumbency).

Let’s see how it works.

```{prf:algorithm}
1. Each agent with a house decides whether to keep their house or enter a lottery.
* Agents who keep their house are done. 
* Houses that are abandoned are available later on.
2. Lottery used to order newcomers and agents who gave up their house (can be completely random or favor particular agents).
3. Serial dictatorship applied using order from lottery and selection from available houses.

```

### Problems

There is a problem. Existing tenants are not guaranteed to get at least as good a house as their current house!
This may cause existing tenants to avoid the lottery risk and the process may fail to take advantage of beneficial trades.
Is there a way to protect existing tenants, enjoy all beneficial trades, and maybe ensure truthfulness, too? Yes!

## Priority Line Mechanism

```{admonition} Intuition
“you request my house – I get your turn”
```
```{prf:algorithm} Priority Line Mechanism
1. All agents are ordered according to some priority
2. Agent with top priority chooses an unassigned house, then second agent, and so on, until someone requests an incumbent’s house. 
3. If the incumbent has already chosen a house, continue. If not, promote the incumbent to just above the requestor and re-start the procedure with the incumbent. 
```
If a cycle forms, it is formed exclusively by incumbents (why?), so let’s clear that cycle and continue with the priority order. 

### Properties of Priority Line
```{prf:theorem}
The Priority Line mechanism is Pareto-efficient, truthful and makes no incumbent tenant worse off.
```
```{prf:proof}
Similar to results we've shown. (Try it!)
```

### Relationship with SD and TTC
* If there are no existing tenants: Priority Line = serial dictatorship. 
* If everyone has a house: Priority Line = TTC. 
* In fact, Priority Line is a version of TTC in which, at each round, every unoccupied house points to the agent with the (current) highest priority.

#### Question
Three people $1, 2, 3$ and houses $A, B, C$ with preferences and ownership:
* $1: A \succ B \succ C$
* $2: A \succ C \succ B$
* $3: B \succ C \succ A$ and $3$ owns $A$

What happens in priority line if priority is $1,2,3$?
```{dropdown} Solution
* $1 \rightarrow A$ (owned by $3$), so $3 \rightarrow B$, match $(3, B)$, $A$ vaccant.
* Then $1 \rightarrow A$, so match $(1, A)$. Leaves $(2, C)$.
* So $\{(1, A), (2, C), (3, B)\}$ is the final matching.
```

```{attention}
Get more practice [here](https://colab.research.google.com/drive/1Iz7YJAlnFs4TQyIgDZDS8MhZUZWmhqQI?usp=sharing)!
```


## Kidney Exchange
Transplants are standard treatment for patients with failed kidneys. Transplants come from two sources
* Cadaveric transplants: donors who have died. 
* Living donor transplants: typically relatives, spouses, etc.

There is a shortage of transplant kidneys. 
* Wait list for a transplant has been getting longer. 
* Over 105,000 patients are on the wait list. 
* Roughly 20,000 transplants a year, mostly cadaveric. 
* In 2018, 9,500 people on the list died or became too sick to receive a transplant. 

### Resolving the Shortage
Buying and selling kidneys is illegal.
Section 301 of National Organ Transplant Act
> “it shall be unlawful for any person to knowingly acquire, receive or otherwise transfer any human organ for valuable consideration for use in human transplantation.”

There are probably ways to increase the supply of cadaveric kidneys (e.g. make donation the default).
We’re going to focus on ways to increase the supply of living donor kidneys.

### Compatability
Donor kidney must be compatible with patient
Blood type match
* O type patients can receive only O kidneys 
* A type patients can receive O or A kidneys 
* B type patients can receive O or B kidneys 
* AB type patients can receive from any blood type
Also tissue type match (HLA compatibility).
Potential inefficiency: if a patient has a donor but can’t use the donor’s kidney, the donor goes home.

### Paired Exchange
Paired exchange: match two donor-patient pairs...
* Donor 1 is compatible with Patient 2, not Patient 1 
* Donor 2 is compatible with Patient 1, not Patient 2

List exchange: match one incompatible donor-patient pair and the waiting list
* Donor of incompatible pair donates to compatible patient nearest the top of the waiting list. 
* Patient of incompatible pair goes to the top of the wait list.

Similar to house allocation with existing tenants.
* The problems are (essentially) equivalent
* TTC can be used to efficiently assign kidneys.

In 2004, RSU helped doctors in Boston to establish first clearinghouse for New England.

### Exchange in Practice
* Moving from theory to practice has some twists 
* US doctors think of compatibility as 0-1, which eliminates strict preference and allows for a different algorithm. 
* Some limits on types of swaps (pairwise, or only 2/3-way). 
* Have to decide how often to clear the market. 
* Participation is a big issue. Compatible donors may not participate. Some hospitals may not participate.

Real-world market design always raises extra issues!

### Donor Chains
In July 2007, Alliance for paired donations started an “Altruistic Donor Chain”
Altruistic donor in Michigan donated kidney to woman in Phoenix.
Husband of Phoenix woman gave kidney to woman in Toledo.
Her mom gave kidney to patient A in Columbus, whose daughter simultaneously gave kidney to patient B in Columbus.
And so on $\ldots$

```{image} ../images/donor-chain.png
:align: center
```
