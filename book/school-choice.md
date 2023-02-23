# School Choice

```{figure} ../images/school-choice.png
:name: school-choice
:height: 400px

_Wanderer above the Sea of Fog_ by Caspar David Friedbrich inpainted with an aerial view of Stanford's campus with DALL-E-2.
```

So far, two approaches to matching problems
* Finding stable outcomes: DA algorithm
* Finding core or Pareto efficient outcomes: serial dictatorship, TTC and Priority Line mechanisms.
		
And applications: entry-level labor markets (residents, law clerks), room/house allocation, kidney exchanges.

Today: applying matching theory to school choice
* Common problem, with interesting open questions. 
* Useful to illustrate trade-offs between different objectives (stability vs. efficient) and different mechanisms (DA vs TTC).

In many countries including the US, children historically have gone to neighborhood schools.
 
In more recent years, many US cities have adopted “school choice” programs, designed to give families additional flexibility, and maybe create some competition between schools.

We’ll discuss how the matching mechanisms we’ve studied inform the design of these programs.

## Objectives

What are the design goals?  

“Efficient” placements

“Fair” procedure and outcomes

Mechanisms that are easy to understand and use.

Promote quality-enhancing competition among schools (?)

Abdulkadiroglu and Sonmez (2003, AER) argued that placement mechanisms used in many cities are badly flawed and proposed alternative mechanisms.

In the following years, gradually, many cities, eg. Boston, New York, Chicago, San Francisco, adopted new mechanisms.

A flurry of research soon followed and still continues
* Designing improved mechanisms & studying the performance of mechanisms in use. 
* Partially random nature of allocations allows causal empirical studies of school effectiveness.

## School Choice Model
Set of students $S$ and schools $C$
* Each student can go to one school 
* Each school $c$ can admit qc students 
* Each student has strict preferences over schools. 
* Each school has a strict “priority order” over students.

This is a “many-to-one” version of the matching model we started with.

## Stability
One notion of a “good” assignment might be an assignment that is stable. 

Stability means: 
: no blocking individual – no student wants to drop out and no school wants to refuse a student.
: no blocking pair – no student can find a school that will accept her, possibly by displacing some other student.

## Stability as Fairness

No blocking individual means no student can be forced to attend a school they don’t want to attend, and no school can be forced to take a student they view as unqualified.

No blocking pair can mean “no justified envy.” That is, no student $s$ prefers school $c$ to her assigned school $c$, when some other student with lower priority is assigned to $c$.

## Boston Mechanism
```{prf:algorithm} Old Boston Mechanism
Each student submits a preference ranking, and each school’s priority order over students is known.
1. Consider the top choices of the students
2. For each school, assign seats to students that ranked it first according to priority order. 
3. Stop if all seats assigned or run out of students ranking it first.
4. Consider remaining students and their second choices. Repeat the above process.
5. Continue with third choices and so on $\ldots$
```

### Problems
```{prf:remark}
The Boston mechanism is not strategy-proof.
```
If you don’t put your priority school high on your rank list, you may lose it! 

Example: you want school A most and B second. You have high priority at B but not A. If a school is in high demand, then to be admitted you need both to rank it first and have high priority. Perhaps you should rank B first.

This was well-understood by Boston parents, and frequently showed up on parent message boards.

```{prf:remark}
The Boston mechanism is also unfair.
```
Doesn't necessarily lead to stable outcomes.
Example: Consider the situation on the prior slide and suppose the family decides to take a risk, puts A first, and then ends up at much less preferred school C. The outcome is not stable because the family has high priority at B and prefers it to C. There is “justified envy.”  
Or, it ranks B first and later learns that it could have gotten into A! 
(Economically) disadvantaged families often don’t know how to game the system.

### Boston in Practice
Students entering in grades K,6,9 and new students submit preferences
Schools have priorities as follows
1. Students already at the school. 
2. Students with a sibling at the school and in the walk zone 
3. Students with a sibling at the school but not in the walk zone 
4. Students in the walk zone 
5. Everyone else
Abdulkadiroglu et al. found that 19% listed two over-demanded schools as top two choices and about a quarter of these students ended up unassigned – ugh! 

## Columbus (OH) Schools
```{prf:algorithm} Columbus Mechanism
1. Each student applies to up to three schools.
2. For some schools, seats are guaranteed based on assignment area.
3. Once those are filled, a lottery is held at each school and offers are made. 
4. A student with an offer has three days to decide. If she says yes, she’s removed from the system.
5. Process repeats. 
```


## (Old) NYC Schools
```{prf:algorithm} Old NYC Mechanism
1. Each student (90,000 plus applying to high schools) can submit up to five applications.
2. Each school receives applications and makes offers, plus it makes a waiting list.
3. Students accept or reject offers.
4. Schools make offers from wait lists (three rounds)
```
Roughly 30,000 students would be unassigned at the end; they would be administratively assigned.

## Student Proposing DA
What about the student proposing DA?
* We know this leads to a stable match: no justified envy. 
* And the stable match that is best for all the students, whose welfare we care about. 
* Plus it’s strategy-proof for the students, and we may not be worried about schools if priorities are clearly stated.
So our earlier results indicate that student-proposing DA has attractive properties, but are there drawbacks?

### Inefficient Stable Matchings

Example [TODO]

TODO: finish lecture 7
