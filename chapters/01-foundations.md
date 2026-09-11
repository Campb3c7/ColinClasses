---
title: Foundations of Probability
---

# 1. Foundations of Probability

## What you have to know

:::{important}
- A probabilistic model describes statistical regularity when exact values or exact
  relationships cannot be known.
- A **sample space** $S$ contains every elementary outcome. An **event** is a subset of $S$.
- Probability is a unit mass distributed across $S$; $P(A)$ is the mass supported on $A$.
- The axioms are nonnegativity, $P(S)=1$, and countable additivity for disjoint events.
- $P(A\mid B)=P(A\cap B)/P(B)$ for $P(B)>0$.
- Independence means $P(A\cap B)=P(A)P(B)$, not that the events are mutually exclusive.
- Bayes' rule reverses the direction of conditioning.
- Repeated independent Bernoulli trials lead to the binomial law; repeated trials with
  more than two outcome categories lead to the multinomial law.
:::

## Why probabilistic models exist

A model is a precise mathematical, logical, or computational representation of how
quantities behave or relate. Deterministic models such as $V=IR$ assume that the
relevant quantities and their relationship can be known precisely.

Many systems do not meet those assumptions. Five-year profit cannot be determined from
this year's infrastructure investment by a law like Ohm's law. Noise affects message
reception; component quality affects reliability; traffic depends statistically on time
of day. In these settings, a useful model relates **statistical attributes** rather than
predicting every value with certainty.

:::{warning}
A statistical relationship does not automatically establish causality. Limited data
can produce false patterns, and a probabilistic model can depend strongly on its
assumptions.
:::

## Experiments, outcomes, sample spaces, and events

- A **random experiment** has random results.
- An **outcome** is one elementary, indivisible result.
- The **sample space** $S$ is the set of all possible outcomes.
- An **event** $A$ is any subset of $S$.
- The certain event is $S$; the null event is $\varnothing$.

For two coin tosses,

$$
S=\{HH,HT,TH,TT\}.
$$

The event “at least one head” is $\{HH,HT,TH\}$. This sample space is finite and
countable. By contrast, a room temperature modeled on an interval such as
$[0^\circ\!F,100^\circ\!F]$ has an uncountable sample space at infinite resolution.

```{mermaid}
flowchart LR
    R[Random experiment] --> O[One outcome]
    R --> S[All outcomes: sample space S]
    S --> A[Event A: a subset of S]
    A --> P[Probability P(A)]
```

## Two interpretations of probability

In the frequentist view, the probability of outcome $k$ is its long-run relative
frequency. If $N_k(n)$ counts occurrences of $k$ in $n$ trials,

$$
P_k=\lim_{n\to\infty}\frac{N_k(n)}{n}.
$$

The axiomatic view assigns numerical probabilities to events while requiring them to
obey the probability axioms. The first view supplies operational intuition; the second
supplies the mathematical rules.

## The probability axioms

For events inside $S$:

1. $P(A)\ge0$ for every $A\subseteq S$.
2. $P(S)=1$.
3. For pairwise-disjoint $A_1,A_2,\ldots$,

$$
P\left(\bigcup_{k=1}^{\infty}A_k\right)
=\sum_{k=1}^{\infty}P(A_k).
$$

The most useful picture is a total probability mass of one spread across every
possibility. An event receives the part of that mass lying inside its region.

### Consequences you should be able to use

$$
0\le P(A)\le1,\qquad P(A^c)=1-P(A),\qquad P(\varnothing)=0.
$$

For two events,

$$
P(A\cup B)=P(A)+P(B)-P(A\cap B).
$$

The subtraction prevents the overlap from being counted twice. More generally,
inclusion–exclusion alternates subtraction and addition over intersections. Also, if
$A\subseteq B$, then $P(A)\le P(B)$.

## Conditional probability

Conditioning restricts attention to the probability mass inside $B$. The probability of
$A$ given $B$ is the fraction of $B$'s mass that also lies in $A$:

$$
P(A\mid B)=\frac{P(A\cap B)}{P(B)},\qquad P(B)>0.
$$

Rearranging gives the multiplication rule

$$
P(A\cap B)=P(A\mid B)P(B).
$$

<details>
<summary>Self-check: Why does the denominator equal P(B)?</summary>

Once $B$ is known to have occurred, $B$ becomes the new universe. Dividing by $P(B)$
renormalizes its probability mass to one.
</details>

## Independence

Events $A$ and $B$ are independent when learning one does not change the probability of
the other:

$$
P(A\mid B)=P(A),\qquad P(B\mid A)=P(B).
$$

Equivalently,

$$
P(A\cap B)=P(A)P(B).
$$

:::{warning} Independence versus mutual exclusion
Mutually exclusive events cannot occur together, so $P(A\cap B)=0$. If independent
events both have positive probability, then $P(A\cap B)=P(A)P(B)>0$. They therefore
cannot be mutually exclusive.
:::

## Bayes' rule

Let $B_1,\ldots,B_n$ partition $S$: their union is $S$ and no two overlap. Then

$$
P(B_j\mid A)
=\frac{P(A\mid B_j)P(B_j)}
{\sum_{k=1}^{n}P(A\mid B_k)P(B_k)}.
$$

The same equation can be read as

$$
\text{posterior}=\frac{\text{likelihood}\times\text{prior}}{\text{evidence}}.
$$

### Satellite-camera example

Suppose a camera sees a green patch. The lecture assigns

$$
P(\text{Water})=0.75,\quad
P(\text{Green}\mid\text{Water})=0.10,\quad
P(\text{Green})=0.20.
$$

Therefore,

$$
P(\text{Water}\mid\text{Green})
=\frac{(0.10)(0.75)}{0.20}=0.375.
$$

The evidence cannot be chosen arbitrarily. Here
$P(\text{Green}\cap\text{Water})=0.075$, so $P(\text{Green})$ cannot be less than
$0.075$.

## Bernoulli trials and the binomial law

A Bernoulli trial has two outcomes, often called success and failure. With
$p=P(\text{success})$, the probability of exactly $k$ successes in $n$ independent
trials is

$$
P_n(k)=\binom{n}{k}p^k(1-p)^{n-k},\qquad k=0,1,\ldots,n.
$$

The three factors have separate jobs: $p^k$ gives the probability of the successes,
$(1-p)^{n-k}$ gives the probability of the failures, and $\binom nk$ counts the orders
in which they can occur.

For three heads in five fair tosses,

$$
P_5(3)=\binom53(0.5)^3(0.5)^2=0.3125.
$$

### A runnable relative-frequency experiment

```{code-cell} python
import random

random.seed(7)
trials = 20_000
hits = 0

for _ in range(trials):
    heads = sum(random.random() < 0.5 for _ in range(5))
    hits += heads == 3

estimate = hits / trials
print(f"Simulation: {estimate:.4f}")
print(f"Exact:      {10 * (0.5 ** 5):.4f}")
```

This connects the frequentist interpretation to the axiomatic calculation: as the
number of trials grows, the simulated relative frequency should settle near $0.3125$.

## Multinomial law

If $B_1,\ldots,B_m$ partition the sample space, $P_k=P(B_k)$, and $r_k$ counts how many
times category $B_k$ occurs in $n$ independent trials, then

$$
P(r_1,\ldots,r_m)
=\frac{n!}{r_1!r_2!\cdots r_m!}
P_1^{r_1}P_2^{r_2}\cdots P_m^{r_m},
$$

where $r_1+\cdots+r_m=n$. The binomial law is the $m=2$ case.

:::{note} Source trace
This chapter follows **Lecture 1: Probability**, especially slides 2–6 (models), 8–12
(definitions and axioms), 13–17 (conditioning, independence, and Bayes), and 18–21
(binomial and multinomial laws).
:::
