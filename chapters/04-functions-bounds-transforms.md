---
title: Functions, Bounds & Transforms
---

# 4. Functions, Bounds & Transforms

## What you have to know

:::{important}
- A function of a random variable, $Y=g(X)$, is another random variable.
- To find the density of $Y$, collect probability from **every** $x$ that maps to the
  same $y$ and account for local stretching with a derivative.
- Markov, Chebyshev, Bienaymé, and Chernoff bounds control tail probabilities using
  progressively richer information about a distribution.
- Transform methods re-express a distribution so moments and sums become easier to study.
- The characteristic function always uses $e^{j\omega X}$; the PGF applies to
  nonnegative integer-valued variables; the Laplace transform applies to nonnegative
  continuous variables; the MGF uses $e^{sX}$ when it exists.
:::

```{mermaid}
flowchart LR
    X[Distribution of X] --> G[Function Y = g(X)]
    X --> B[Tail bounds]
    X --> T[Transforms]
    G --> FY[Distribution of Y]
    B --> M[Markov / Chebyshev / Chernoff]
    T --> C[Characteristic function]
    T --> P[Probability generating function]
    T --> L[Laplace transform]
    T --> Q[Moment generating function]
```

## Functions of random variables

If $Y=g(X)$, an event involving $Y$ can be rewritten as an **equivalent event** involving
$X$. For example, the set of input values satisfying $g(X)\le a$ may consist of several
separate intervals. Their probabilities add because each interval maps into the same
output event.

The expectation of a function can be found without first deriving the distribution of
$Y$:

$$
E[g(X)] = \int_{-\infty}^{\infty} g(x)f_X(x)\,dx.
$$

### Density transformation

Suppose the equation $y=g(x)$ has solutions $x_1,x_2,\ldots,x_n$. Then

$$
f_Y(y)=\sum_k f_X(x_k)\left|\frac{dx}{dy}\right|_{x=x_k}
=\sum_k \frac{f_X(x_k)}{|dy/dx|_{x=x_k}}.
$$

The sum handles a many-to-one map. The derivative handles stretching: where a small
input interval spreads across a large output interval, the output density must decrease.

For the linear case $Y=aX+b$ with $a\ne0$,

$$
f_Y(y)=\frac{1}{|a|}f_X\left(\frac{y-b}{a}\right).
$$

:::{tip} A reliable change-of-variables routine
1. Solve $y=g(x)$ for every valid input $x_k$.
2. Evaluate $f_X(x_k)$ at each solution.
3. Divide each contribution by $|g'(x_k)|$.
4. Add the contributions and state the support of $Y$.
:::

## Expectation and variance facts

For a constant $c$,

$$
E[c]=c,\qquad E[cX]=cE[X],\qquad E[X+c]=E[X]+c,
$$

$$
\operatorname{Var}(c)=0,\qquad
\operatorname{Var}(cX)=c^2\operatorname{Var}(X),\qquad
\operatorname{Var}(X+c)=\operatorname{Var}(X).
$$

For a transformed variable,

$$
\operatorname{Var}(g(X))
=E\left[(g(X)-E[g(X)])^2\right].
$$

The contrast is worth remembering: adding a constant moves the center but does not
change the spread; multiplying by $c$ multiplies standard deviation by $|c|$ and
variance by $c^2$.

## Shape: skew and kurtosis

The standardized third central moment measures asymmetry:

$$
\operatorname{Skew}(X)=E\left[\left(\frac{X-E[X]}{\sigma_X}\right)^3\right].
$$

- Negative skew means the left tail is larger.
- Zero skew means symmetric tails.
- Positive skew means the right tail is larger.

The lecture defines excess kurtosis by

$$
\operatorname{Kurtosis}(X)
=E\left[\left(\frac{X-E[X]}{\sigma_X}\right)^4\right]-3.
$$

Subtracting $3$ makes the Gaussian's excess kurtosis equal to zero.

## Bounds on tail probabilities

### Markov inequality

For $X\ge0$ and $a>0$,

$$
P(X\ge a)\le \frac{E[X]}{a}.
$$

It uses only nonnegativity and the mean, so it is broad but often loose. It becomes
informative only when $a>E[X]$.

### Chebyshev and Bienaymé inequalities

If $m=E[X]$ and $\sigma^2=\operatorname{Var}(X)$,

$$
P(|X-m|\ge a)\le\frac{\sigma^2}{a^2},
$$

or, setting $a=k\sigma$,

$$
P(|X-m|\ge k\sigma)\le\frac{1}{k^2}.
$$

Thus the probability of lying at least four standard deviations from the mean is at
most $1/16$.

The lecture's more general Bienaymé form is

$$
P(|X-b|\ge a)\le\frac{E[|X-b|^n]}{a^n},
\qquad a>0,\ n\ge2.
$$

Chebyshev is the special case $b=m$ and $n=2$.

### Chernoff bound

The key idea is to upper-bound the indicator of the event $X\ge a$ by an exponential.
For any $s>0$,

$$
P(X\ge a)\le e^{-sa}E[e^{sX}].
$$

Choosing the $s$ that minimizes the right-hand side tightens the bound. If
$X=\sum_i X_i$ and the $X_i$ are independent, then

$$
E[e^{sX}]=\prod_i E[e^{sX_i}],
$$

which explains why the Chernoff method is especially useful for sums.

<details>
<summary>Self-check: Which bound can you use with only a nonnegative variable and its mean?</summary>

Markov. Chebyshev additionally needs the variance, while Chernoff uses an exponential
moment.
</details>

## Transform methods

Transforms help calculate moments, analyze sums, establish properties such as stability,
and simplify distribution calculations.

### Characteristic function

With $j=\sqrt{-1}$,

$$
\Phi_X(\omega)=E[e^{j\omega X}]
=\int_{-\infty}^{\infty}f_X(x)e^{j\omega x}\,dx.
$$

The inverse relation is

$$
f_X(x)=\frac{1}{2\pi}\int_{-\infty}^{\infty}
\Phi_X(\omega)e^{-j\omega x}\,d\omega.
$$

For a discrete random variable,

$$
\Phi_X(\omega)=\sum_k p_X(x_k)e^{j\omega x_k}.
$$

For an integer-valued variable, the characteristic function is periodic and

$$
p_X(k)=\frac{1}{2\pi}\int_0^{2\pi}\Phi_X(\omega)e^{-j\omega k}\,d\omega.
$$

Scaling the variable scales the transform argument: if $Y=aX$, then
$\Phi_Y(\omega)=\Phi_X(a\omega)$.

When the required derivatives and moments exist,

$$
E[X^n]=\frac{1}{j^n}
\left.\frac{d^n}{d\omega^n}\Phi_X(\omega)\right|_{\omega=0}.
$$

### Probability generating function

For a nonnegative integer-valued random variable $N$,

$$
G_N(z)=E[z^N]=\sum_{k=0}^{\infty}p_N(k)z^k.
$$

It generates the PMF through

$$
p_N(k)=\frac{1}{k!}\left.\frac{d^k}{dz^k}G_N(z)\right|_{z=0}.
$$

It also generates moments at $z=1$:

$$
G_N'(1)=E[N],\qquad G_N''(1)=E[N(N-1)],
$$

$$
\operatorname{Var}(N)=G_N''(1)+G_N'(1)-[G_N'(1)]^2.
$$

### Laplace transform and moment generating function

For a nonnegative continuous random variable,

$$
X^*(s)=E[e^{-sX}]=\int_0^{\infty}f_X(x)e^{-sx}\,dx,
$$

and

$$
E[X^n]=(-1)^n\left.\frac{d^n}{ds^n}X^*(s)\right|_{s=0}.
$$

The general moment generating function is

$$
\Theta_X(s)=E[e^{sX}]
=\int_{-\infty}^{\infty}e^{sx}f_X(x)\,dx.
$$

If it exists near $s=0$, then

$$
E[X^n]=\left.\frac{d^n}{ds^n}\Theta_X(s)\right|_{s=0}.
$$

:::{note} Source trace
This chapter follows **Lecture 4: Functions, Bounds, and Transformations**, especially
slides 3–6 (functions), 8–12 (shape and bounds), and 14–25 (transform methods).
:::
