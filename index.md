---
title: Probability & Random Processes
---

# Probability & Random Processes — Study Companion

An interactive companion for [your course], organized around **what you have to know**.
Each unit explains the concept, why it matters, and pairs it with a visualization or a
simulation you can run yourself.

:::{important} This book is a scaffold.
The chapter skeletons and outlines below are a draft based on a standard
Probability & Random Processes curriculum. They will be **filled in from your actual
lecture notes** as we work through them together.
:::

## The course map

Everything in a typical Probability & Random Processes course hangs together like this:

```{mermaid}
flowchart TD
    A[Probability Foundations] --> B[Random Variables]
    B --> D[Joint Distributions & Conditioning]
    B --> C[Important Distributions]
    C --> D
    D --> E[LLN & Central Limit Theorem]
    C --> E
    D --> F[Random Processes]
    F --> G[Poisson Processes]
    F --> H[Markov Chains]
```

## Units

1. **Foundations of Probability** — sample spaces, events, axioms, counting,
   conditioning, independence, Bayes' rule.
2. **Random Variables** — PMFs, PDFs, CDFs, expectation, variance, transformations.
3. **Important Distributions** — Bernoulli, binomial, geometric, Poisson, uniform,
   exponential, Gaussian, and when each one shows up in the wild.
4. **Joint Distributions & Conditioning** — joint PMFs/PDFs, covariance, correlation,
   conditional distributions, independent random variables.
5. **LLN & Central Limit Theorem** — convergence facts, why averages stabilize, why the
   Gaussian shows up everywhere.
6. **Random Processes** — the idea of a random signal, iid processes, stationarity.
7. **Poisson Processes** — counting events in time, interarrival times, merging/splitting.
8. **Markov Chains** — states, transition matrices, stationary distributions.

## How to use this book

- **Read a unit** → each one opens with the *must-know* facts, then the *why*, then visuals.
- **Run the simulations** → every computational figure embeds executable Python; tweak the
  numbers and watch the picture change.
- **Browse dropdowns & cards** → interactive elements break the density of math into
  digestible pieces.

## Roadmap

- [x] Site infrastructure (this book, GitHub Pages deployment)
- [ ] Course map finalized against your actual syllabus
- [ ] Unit content written from your lecture notes
- [ ] Interactive visualizations for every major concept