---
title: Scalar Random Variables
---

# 2. Scalar Random Variables

## What you have to know

:::{important}
- A random variable $X:S\to\mathbb{R}$ is a deterministic function that assigns a number
  to each outcome.
- The CDF $F_X(x)=P(X\le x)$ works for every random variable.
- A discrete variable is described by a PMF; a continuous variable is described by a PDF;
  a mixed variable has both jumps and continuous growth in its CDF.
- Probability equals PMF mass at points or PDF area over intervals.
- $E[X]$ locates the center; $\operatorname{Var}(X)$ measures squared spread around it.
- A jump in the CDF at $a$ has size $P(X=a)$.
- Conditioning replaces the original distribution with one restricted to an event.
:::

```{mermaid}
flowchart LR
    S[Outcome ξ in S] --> X[Number X(ξ)]
    X --> C[CDF: always available]
    X --> D{Type}
    D --> P[Discrete: PMF]
    D --> F[Continuous: PDF]
    D --> M[Mixed: masses + density]
```

## A random variable is a map

The experiment produces an outcome $\xi$. The random variable applies a fixed rule to
that outcome:

$$
X:S\longrightarrow\mathbb{R},\qquad \xi\longmapsto X(\xi).
$$

The function itself is deterministic. The uncertainty comes from not knowing which
outcome the experiment will produce.

For three coin tosses, one possible rule substitutes $H=1$ and $T=0$ and reads the
result as a binary number. Then $X(HHH)=7$, $X(TTT)=0$, and $X(HTH)=5$. A different
rule could count heads. The same outcome $HTH$ would then map to $2$.

:::{tip}
Always separate the outcome from the number assigned to it. The sample space contains
outcomes; the range $S_X$ contains possible values of the random variable.
:::

## The cumulative distribution function

The CDF records how probability accumulates:

$$
F_X(x)=P(X\le x)
=P(\{\xi:X(\xi)\le x\}),\qquad -\infty<x<\infty.
$$

Every CDF satisfies

$$
0\le F_X(x)\le1,
$$

$$
\lim_{x\to-\infty}F_X(x)=0,
\qquad
\lim_{x\to\infty}F_X(x)=1,
$$

and it is nondecreasing and right-continuous. Interval probabilities come from
subtracting accumulated mass:

$$
P(a<X\le b)=F_X(b)-F_X(a),\qquad a\le b.
$$

The jump at $a$ equals the point mass:

$$
P(X=a)=F_X(a)-F_X(a^-).
$$

If the CDF is continuous at $a$, then $P(X=a)=0$. When it is continuous at both
endpoints, including or excluding those endpoints does not change the interval
probability.

### Heads in three tosses

Let $X$ count the heads in three fair tosses. Its PMF is

| $x$ | 0 | 1 | 2 | 3 |
|---:|---:|---:|---:|---:|
| $P(X=x)$ | $1/8$ | $3/8$ | $3/8$ | $1/8$ |

The CDF is a staircase: it jumps by the PMF value at each possible $x$.

```{code-cell} python
from fractions import Fraction

pmf = {0: Fraction(1, 8), 1: Fraction(3, 8),
       2: Fraction(3, 8), 3: Fraction(1, 8)}
running = Fraction(0)
for x, mass in pmf.items():
    running += mass
    print(f"F({x}) = {running}")
```

<details>
<summary>Self-check: What is P(1 &lt; X ≤ 3)?</summary>

$F_X(3)-F_X(1)=1-1/2=1/2$.
</details>

## Discrete, continuous, and mixed variables

- A **discrete** variable has a staircase CDF. Its probability lives at isolated points.
- A **continuous** variable has a continuous CDF. Its probability accumulates smoothly.
- A **mixed** variable combines jumps with continuous growth.

The CDF is the common language across all three types.

## PMF and PDF

For a discrete variable with range $S_X=\{x_1,x_2,\ldots\}$, the probability mass
function is

$$
p_X(x_k)=P(X=x_k),\qquad x_k\in S_X.
$$

For a differentiable CDF, the probability density function is

$$
f_X(x)=\frac{d}{dx}F_X(x).
$$

For very small $h$,

$$
P(x<X\le x+h)\approx h f_X(x).
$$

The exact interval rule is

$$
P(a\le X\le b)=\int_a^b f_X(x)\,dx,
$$

and

$$
F_X(x)=\int_{-\infty}^{x}f_X(s)\,ds.
$$

A valid PDF satisfies $f_X(x)\ge0$ and

$$
\int_{-\infty}^{\infty}f_X(x)\,dx=1.
$$

If a nonnegative function $g$ has finite integral
$c=\int_{-\infty}^{\infty}g(x)\,dx$, then $f_X(x)=g(x)/c$ is normalized into a PDF.

:::{warning} Density is not point probability
For a continuous variable, $f_X(x)$ is a density height. Probability comes from area,
and $P(X=x)=0$ at every single point.
:::

The lecture also represents a discrete PMF as impulses:

$$
f_X(x)=\sum_k p_X(x_k)\delta(x-x_k),
$$

whose integral produces the staircase CDF.

## Mean, variance, and moments

The mean, or expected value, is

$$
E[X]=\int_{-\infty}^{\infty}x f_X(x)\,dx
$$

for a continuous variable, and

$$
E[X]=\sum_k x_k p_X(x_k)
$$

for a discrete variable.

Expectation requires absolute integrability:

$$
E[|X|]<\infty.
$$

The variance and standard deviation are

$$
\sigma_X^2=\operatorname{Var}(X)
=E[(X-E[X])^2]
=E[X^2]-(E[X])^2,
$$

$$
\sigma_X=\sqrt{\operatorname{Var}(X)}.
$$

The $n$th raw, central, absolute, and generalized moments about $a$ are respectively

$$
E[X^n],\qquad E[(X-E[X])^n],\qquad E[|X|^n],\qquad E[(X-a)^n].
$$

## Conditional distributions

Given an event $A\subseteq S$ with $P(A)>0$, the conditional CDF is

$$
F_X(x\mid A)
=\frac{P(\{X\le x\}\cap A)}{P(A)}.
$$

When differentiable,

$$
f_X(x\mid A)=\frac{d}{dx}F_X(x\mid A).
$$

Conditioning trims away outcomes outside $A$ and then renormalizes the remaining
probability to total one. For example, conditioning a fair die on “$X$ is even” leaves
only $2,4,6$, each with conditional mass $1/3$.

:::{note} Source trace
This chapter follows **Lecture 2: Scalar Random Variables**, slides 2–4 (random-variable
maps and the CDF), 5–10 (CDF properties, types, PMFs, and PDFs), and 11–15 (examples,
expectation, variance, moments, and conditional distributions).
:::
