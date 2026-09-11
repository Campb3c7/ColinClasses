---
title: Common Random Variables
---

# 3. Common Random Variables

## What you have to know

:::{important}
- **Binomial:** successes in a fixed number of independent Bernoulli trials.
- **Geometric:** trials until the first success, or failures before it.
- **Poisson:** the number of independent random events in an interval; its parameter is
  the expected count $\alpha=\lambda T$.
- **Exponential:** the time between Poisson events; it is continuous and memoryless.
- **Gaussian:** the bell-shaped distribution; standardize with $(X-m)/\sigma$.
- **Gamma:** a flexible positive distribution that includes exponential, chi-square,
  and Erlang special cases.
- **Beta:** a flexible distribution restricted to $0<x<1$.
- **Zipf and Pareto:** power-law distributions with moments that may diverge.
:::

```{mermaid}
flowchart TD
    B[Bernoulli trials] --> BI[Binomial count]
    B --> G[Geometric waiting trials]
    BI -->|many trials, small p| P[Poisson count]
    P --> E[Exponential interarrival time]
    BI -->|large n| N[Gaussian approximation]
    E --> GA[Gamma / Erlang waiting time]
    Z[Zipf: discrete power law] --> PA[Pareto: continuous power law]
```

## Discrete random variables

### Binomial

For $X\sim\operatorname{Binomial}(n,p)$,

$$
S_X=\{0,1,\ldots,n\},\qquad
P(X=k)=\binom nk p^k(1-p)^{n-k}.
$$

It answers: **How many successes occur in $n$ independent trials when every trial has
success probability $p$?** Increasing $p$ moves the mass toward larger counts.

### Geometric

The lecture uses two conventions:

| Convention | Meaning | Support | PMF |
|---|---|---|---|
| Type I | number of trials until success | $k=1,2,\ldots$ | $p(1-p)^{k-1}$ |
| Type II | number of failures before success | $k=0,1,\ldots$ | $p(1-p)^k$ |

The two variables differ by one. State the convention before doing any calculation.

### Poisson

For $X\sim\operatorname{Poisson}(\alpha)$,

$$
S_X=\{0,1,2,\ldots\},\qquad
P(X=k)=\frac{\alpha^k}{k!}e^{-\alpha},\quad \alpha>0.
$$

It models a count of events that occur randomly and independently in an interval or
set. If events arrive at rate $\lambda$ during an interval of size $T$, then

$$
\alpha=\lambda T.
$$

The events are discrete even when the time or space in which they occur is continuous.
Examples from the lecture include device failures per year, communication errors, and
failed components in a large system.

### Poisson approximation to the binomial

For many Bernoulli trials with small $p$, keep $\alpha=np$ fixed. Then

$$
\binom nk p^k(1-p)^{n-k}
\approx \frac{\alpha^k}{k!}e^{-\alpha}.
$$

The following simulation compares both models using only Python's standard library.

```{code-cell} python
from math import comb, exp, factorial

n, p = 100, 0.03
alpha_ = n * p
print(" k   Binomial   Poisson")
for k in range(9):
    binomial = comb(n, k) * p**k * (1-p)**(n-k)
    poisson = alpha_**k * exp(-alpha_) / factorial(k)
    print(f"{k:2d}   {binomial:0.5f}    {poisson:0.5f}")
```

### Zipf and generalized Zipf

Classic Zipf behavior says frequency is inversely proportional to rank: the $k$th-ranked
item has probability proportional to $1/k$. An infinite classic Zipf distribution cannot
be normalized because the harmonic series diverges.

The generalized Zipf, or zeta, distribution is

$$
p_k=\frac{1}{\zeta(\alpha)}\frac{1}{k^\alpha},
\qquad
\zeta(\alpha)=\sum_{j=1}^{\infty}\frac{1}{j^\alpha}.
$$

- The distribution exists only for $\alpha>1$.
- Its mean exists only for $\alpha>2$.
- Its second moment and variance exist only for $\alpha>3$.

This is a warning about heavy tails: a valid distribution need not have a finite mean or
variance.

## Continuous random variables

### Uniform

For a uniform variable on $[a,b]$,

$$
f_X(x)=\frac{1}{b-a},\qquad a\le x\le b,quad a<b,
$$

and the density is zero outside that interval. Its constant height represents equal
density across equal-length subintervals.

### Exponential

For $X\sim\operatorname{Exponential}(\lambda)$,

$$
f_X(x)=\lambda e^{-\lambda x},\qquad x\ge0, \lambda>0,
$$

$$
F_X(x)=1-e^{-\lambda x}.
$$

It models interarrival times between Poisson events of rate $\lambda$:

$$
E[X]=\frac1\lambda,qquad
\operatorname{Var}(X)=\frac1{\lambda^2},\qquad
\sigma_X=\frac1\lambda.
$$

The coefficient of variation is

$$
\operatorname{CV}[X]=\frac{\sigma_X}{E[X]}=1.
$$

#### Why Poisson counts produce exponential waits

If $N$ counts events during time $t$, then its Poisson parameter is $\alpha=\lambda t$.
No event occurs with probability

$$
P(N=0)=e^{-\lambda t}.
$$

The waiting time $T$ exceeds $t$ exactly when no event has occurred by $t$, so

$$
P(T>t)=e^{-\lambda t},\qquad
P(T\le t)=1-e^{-\lambda t}.
$$

#### Memorylessness

A random variable is memoryless when

$$
P(X>x+h\mid X>x)=P(X>h),\qquad h>0.
$$

The geometric distribution is the only memoryless discrete distribution, and the
exponential distribution is the only memoryless continuous distribution. For an
exponential variable,

$$
\frac{P(X>x+h)}{P(X>x)}
=\frac{e^{-\lambda(x+h)}}{e^{-\lambda x}}
=e^{-\lambda h}.
$$

<details>
<summary>Self-check: A component has survived for x hours. Does that change its exponential model for the next h hours?</summary>

No. Under the exponential model, the conditional survival probability for the next
$h$ hours equals the original survival probability over $h$ hours.
</details>

### Gaussian

A Gaussian, or normal, random variable with mean $m$ and standard deviation $\sigma$ has

$$
f_X(x)=\frac{1}{\sqrt{2\pi}\sigma}
\exp\left[-\frac{(x-m)^2}{2\sigma^2}\right].
$$

There is no elementary closed form for its CDF. Standardization converts it to a
zero-mean, unit-variance random variable:

$$
Y=\frac{X-m}{\sigma}.
$$

The lecture writes the standard Gaussian CDF as

$$
G(y)=\frac{1}{\sqrt{2\pi}}
\int_{-\infty}^{y}e^{-t^2/2}\,dt,
$$

so

$$
F_X(x)=G\left(\frac{x-m}{\sigma}\right).
$$

#### De Moivre–Laplace approximation

When $np(1-p)\gg1$, a binomial PMF can be approximated by a Gaussian density with
$m=np$ and $\sigma^2=np(1-p)$:

$$
\binom nk p^k(1-p)^{n-k}
\approx
\frac{1}{\sqrt{2\pi np(1-p)}}
\exp\left[-\frac{(k-np)^2}{2np(1-p)}\right].
$$

## Flexible positive and bounded families

### Gamma

Using shape $\alpha$ and rate $\lambda$,

$$
f_X(x)=\frac{\lambda(\lambda x)^{\alpha-1}e^{-\lambda x}}
{\Gamma(\alpha)},
\qquad x>0, \alpha>0, \lambda>0,
$$

where

$$
\Gamma(z)=\int_0^\infty s^{z-1}e^{-s}\,ds,
\qquad
\Gamma(z+1)=z\Gamma(z).
$$

Its mean and variance are

$$
E[X]=\frac{\alpha}{\lambda},\qquad
\operatorname{Var}(X)=\frac{\alpha}{\lambda^2}.
$$

Writing $\theta=1/\lambda$ gives the scale form

$$
f_X(x)=\frac{x^{\alpha-1}e^{-x/\theta}}
{\theta^\alpha\Gamma(\alpha)}.
$$

Special cases in the lecture are exponential ($\alpha=1$), chi-square
($\lambda=1/2$, $\alpha=k/2$), and $m$-Erlang ($\alpha=m$). The time to the $m$th
Poisson event is $m$-Erlang.

### Beta

For $0<x<1$ and $\alpha,\beta>0$,

$$
f_X(x)=\frac{\Gamma(\alpha+\beta)}
{\Gamma(\alpha)\Gamma(\beta)}
x^{\alpha-1}(1-x)^{\beta-1}.
$$

Its mean and variance are

$$
E[X]=\frac{\alpha}{\alpha+\beta},
\qquad
\operatorname{Var}(X)=
\frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}.
$$

The beta family changes shape while remaining on a bounded interval. The lecture notes
its use for modeling an uncertain Bernoulli probability $p$.

### Pareto

The Pareto distribution is the continuous counterpart of Zipf. For minimum value $x_m$,

$$
P(X>x)=
\begin{cases}
1, & x<x_m,\\
(x_m/x)^\alpha, & x\ge x_m,
\end{cases}
$$

$$
F_X(x)=
\begin{cases}
0, & x<x_m,\\
1-(x_m/x)^\alpha, & x\ge x_m,
\end{cases}
$$

and

$$
f_X(x)=
\begin{cases}
0, & x<x_m,\\
\alpha x_m^\alpha/x^{\alpha+1}, & x\ge x_m.
\end{cases}
$$

Its mean exists only for $\alpha>1$ and equals
$\alpha x_m/(\alpha-1)$. Its variance exists only for $\alpha>2$ and equals

$$
\operatorname{Var}(X)=
\frac{\alpha x_m^2}{(\alpha-1)^2(\alpha-2)}.
$$

:::{note} Source trace
This chapter follows **Lecture 3: Some Common Random Variables**, slides 3–15
(discrete distributions and Zipf), 17–25 (uniform, exponential, Gaussian, and the
De Moivre–Laplace approximation), and 26–33 (gamma, beta, and Pareto).
:::
