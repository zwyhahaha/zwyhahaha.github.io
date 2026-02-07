---
layout:     post
title:      Asymptotic Memoryless of Markov Chains
subtitle:   
date:       2026-02-06
author:     Wanyu Zhang
header-img: img/post-bg-coffee.jpeg
catalog:    true
tags:
    - Lecture Notes
---

This is the first post in a series of notes taken from the **Stochastic Systems** class (MS&E 321) taught by Professor Peter Glynn. This series will be updated as the course progresses.

A fundamental property of Markov chains is that their long-run behavior "forgets" the initial state. More precisely, for a finite, irreducible, aperiodic Markov chain with transition matrix $P$, the $n$-step transition probabilities $P^n(x,y)$ converge to a stationary distribution $\pi(y)$ at a geometric rate. The key idea behind the proof is a clean algebraic decomposition $P^m = \delta \Lambda + (1-\delta)Q$, which separates a "memoryless" rank-1 component $\Lambda$ from a remainder $Q$. This decomposition admits a natural probabilistic interpretation via coupling, and extends to non-stationary transitions, infinite state spaces, and continuous state spaces through Doeblin's condition.

## Setup

Consider a Markov chain (MC) with:

- Finite state space: $\lvert S\rvert = d < \infty$
- Stationary transition matrix $P$
- $P$ is irreducible and aperiodic

We begin with a technical lemma that connects irreducibility and aperiodicity to a uniform positivity condition on $P^m$.

> **Lemma 1.** Let $P$ be the transition matrix of an irreducible Markov chain on a finite state space $S$. Then $P$ is aperiodic if and only if there exists $m \geq 1$ such that $P^m(x,y) > 0$ for all $x, y \in S$.

*Remark.* This lemma guarantees the existence of $m$ such that $P^m \gg 0$ (all entries strictly positive), which is the starting point of the convergence analysis below. We will revisit the necessity of finiteness in Lemma 1 at the end of this note.

## Convergence Analysis

We first consider the case $m = 1$, i.e., $P \gg 0$.

**1. Decomposition of $P$**

Let $\Lambda$ be a **stochastic matrix** ($\Lambda \mathbf{e} = \mathbf{e}$) with **identical rows**, i.e., $\Lambda = \begin{bmatrix} \lambda \\\\ \vdots \\\\ \lambda \end{bmatrix}$ where $\lambda\  \mathbf{e}= 1$.

Since $P \gg 0$, there exists $\delta \in (0,1)$ such that $P \geq \delta \Lambda$. Define

$$
P = \delta \Lambda + (1 - \delta) Q, \qquad Q = \frac{P - \delta \Lambda}{1 - \delta}.
$$

Then $Q \geq 0$, and $Q$ is stochastic: $Q\mathbf{e} = \frac{P\mathbf{e} - \delta \Lambda\mathbf{e}}{1 - \delta}= \mathbf{e}$.

*Remark.* The parameter $\delta$ measures how much of $P$ can be "explained" by the memoryless component $\Lambda$. A larger $\delta$ means faster mixing.

**2. Computing powers of $P$**

A key property: $R\Lambda = \Lambda$ for any stochastic matrix $R$, since $R\Lambda = R \mathbf{e} \lambda = \mathbf{e} \lambda = \Lambda$.

Expanding $P^2$:

$$
\begin{aligned}
P^2 &= P(\delta \Lambda + (1 - \delta)Q) \\
&= \delta \Lambda + (1 - \delta)PQ \\
&= \delta \Lambda + (1 - \delta)(\delta \Lambda + (1 - \delta)Q)Q \\
&= \delta \Lambda + (1 - \delta)\delta \Lambda Q + (1 - \delta)^2 Q^2
\end{aligned}
$$

By induction, the general formula is:

$$P^n = \sum_{j=0}^{n-1}\delta(1 - \delta)^{j}\Lambda Q^{j} + (1-\delta)^n Q^n.$$

As $n \to \infty$, the remainder $(1-\delta)^n Q^n \to 0$, and:

$$
P^n \to \sum_{j=0}^{\infty} \delta(1 - \delta)^j \Lambda Q^j \quad \triangleq \quad \Pi.
$$

**3. Structure of $\Pi$**

- $\Pi$ is **stochastic**: since $Q^j\mathbf{e} = \mathbf{e}$ for all $j$, we have $\Lambda Q^j\mathbf{e} = \Lambda\mathbf{e} = \mathbf{e}$, and the geometric series preserves row sums.
- $\Pi$ has **identical rows**: since $\Lambda Q^j= \mathbf{e} (\lambda Q^j)$, every term in the series has identical rows.

Therefore $\Pi$ is a rank-1 stochastic matrix whose common row is the stationary distribution $\pi$.

**4. Rate of convergence**

Define the matrix operator norm induced by the $\ell_\infty$ vector norm. For any stochastic matrix $P$, $\lVert P\rVert = 1$. Then:

$$
\lVert P^n - \Pi\rVert = O\!\left((1 - \delta)^n\right) \qquad \text{(rate of mixing)}
$$

**5. Generalization to $m > 1$**

By Lemma 1, for a finite irreducible aperiodic chain, there exists $m$ such that $P^m \gg 0$. Applying the $m=1$ argument to $P^m$ yields

$$
P^{m\,k} \to \Pi := \sum_{j=0}^\infty \delta(1-\delta)^j \Lambda Q^j,
\qquad
\lVert\,P^{m\,k}-\Pi\,\rVert = O\!\left((1-\delta)^k\right).
$$

For general $n$, write $n=km+r$ with $0\le r<m$. Then $P^n = (P^m)^k P^r$. Since $\Pi$ has identical rows, $\Pi P^r = \Pi$, so:

$$
\lVert P^n-\Pi\rVert = \lVert(P^{mk}-\Pi)P^r\rVert \leq \lVert P^{mk}-\Pi\rVert= O\!\left((1-\delta)^k\right).
$$

## Generalizations and Doeblin's Condition

The convergence analysis relies entirely on the decomposition $P^m = \delta \Lambda + (1 - \delta) Q$. This decomposition admits a natural probabilistic interpretation and extends to several broader settings.

**Probabilistic Interpretation (Coupling).** At each block of $m$ steps, with probability $\delta$, the chain "forgets" its past and transitions according to the memoryless kernel $\Lambda$; with probability $1-\delta$, it follows the residual kernel $Q$. The number of blocks until the first "reset" is geometric with parameter $\delta$, which directly gives the exponential mixing rate.

**Non-Stationary Transitions.**
Transition matrices $P(1), P(2), \ldots$ may vary over time, so we do **not** expect a stationary equilibrium. However, if a **uniform lower bound** holds:

$$P(i, x, y) \geq \delta \lambda(y), \quad \forall\, x \in S,\; i \geq 1,$$

then each $P(i) = \delta \Lambda + (1 - \delta) Q_i$, and the same telescoping argument applies:

$$
\begin{aligned}
P(1)P(2) &= P(1)\bigl(\delta \Lambda + (1 - \delta)Q_2\bigr) = \delta \Lambda + (1 - \delta) P(1) Q_2 \\
&= \delta \Lambda + (1 - \delta)\delta \Lambda Q_2 + (1 - \delta)^2 Q_1 Q_2.
\end{aligned}
$$

In general, $\lVert P(1) \cdots P(n) - \text{(rank-1)}\rVert \to 0$ at a geometric rate, even without stationarity.

**Infinite Discrete State Space.**
For $\lvert S\rvert = \infty$, Lemma 1 may fail (see discussion below), so the decomposition $P^m \gg 0$ cannot be guaranteed. One must instead directly assume **Doeblin's condition**: there exist $m$, $\delta > 0$, and a probability measure $\lambda$ such that $P^m(x, \cdot) \geq \delta \lambda(\cdot)$ for all $x \in S$.

**Continuous State Space.**
Doeblin's condition generalizes naturally: assume there exist $m$, $\delta > 0$, and a probability measure $\lambda$ on $(S, \mathcal{B})$ such that

$$\mathbb{P}_x(X_m \in B) \geq \delta \lambda(B), \quad \forall\, x \in S,\; B \in \mathcal{B}.$$

Then $\lvert\mathbb{P}_x(X_n \in B) - \pi(B)\rvert = O(r^n)$ for some $r < 1$, where $\pi$ is the unique stationary measure.

## Discussion on Lemma 1

Recall Lemma 1: *$P$ is irreducible and aperiodic on a finite state space if and only if $\exists\, m$ such that $P^m(x,y) > 0$ for all $x,y$.*

This equivalence relies critically on **finiteness** of the state space. For infinite state spaces, an irreducible aperiodic chain may have no $m$ for which $P^m \gg 0$.

**Counterexample: Birth-death chain.**
Consider the chain on $\lbrace 0, 1, 2, \ldots\rbrace$ with nearest-neighbor transitions. Starting from state $s$, in any finite number of steps $m$, the chain can reach at most state $s + m$, so $P^m(s, s+m+1) = 0$ for all $m$. Hence no single $m$ makes $P^m$ uniformly positive, even though the chain is irreducible and aperiodic.

This is precisely why Doeblin's condition must be imposed as an additional assumption in the infinite state space setting.
