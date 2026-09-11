---
title: Probability & Random Processes
---

# Probability & Random Processes — Study Companion

An interactive companion built directly from Lectures 1–4. Each unit starts with the
facts you have to know, then develops the intuition behind them with worked examples,
concept maps, self-checks, and simulations.

:::{important} Source boundary
The material here comes from the four supplied lecture decks. Topics from later parts
of a typical probability and random-processes course are intentionally absent until
the matching course notes are supplied.
:::

## The course map

The four lectures build on one another like this:

```{mermaid}
flowchart TD
    A[1. Probability foundations] --> B[2. Scalar random variables]
    B --> C[3. Common distributions]
    B --> D[4. Functions of random variables]
    C --> D
    D --> E[Bounds and transform methods]
```

## Units

1. [**Foundations of Probability**](chapters/01-foundations.md) — models, sample spaces,
   events, axioms, conditioning, independence, Bayes' rule, and repeated trials.
2. [**Scalar Random Variables**](chapters/02-random-variables.md) — random-variable maps,
   CDFs, PMFs, PDFs, expectation, variance, moments, and conditioning.
3. [**Common Random Variables**](chapters/03-important-distributions.md) — binomial,
   geometric, Poisson, Zipf, uniform, exponential, Gaussian, gamma, beta, and Pareto.
4. [**Functions, Bounds & Transforms**](chapters/04-functions-bounds-transforms.md) —
   change of variables, skew, kurtosis, probability bounds, characteristic functions,
   PGFs, Laplace transforms, and MGFs.

## How to use this book

- Start with each chapter's **What you have to know** box.
- Open the self-check answers only after working the question yourself.
- Copy a simulation into Jupyter, run it, then change its parameters and compare the result.
- Use the source note at the end of each chapter to return to the exact lecture slides.

## Roadmap

- [x] Site infrastructure and GitHub Pages deployment
- [x] Lectures 1–4 organized into four course units
- [x] Core explanations, formulas, concept maps, self-checks, and simulations
- [ ] Later lectures, added only when their course materials are supplied
