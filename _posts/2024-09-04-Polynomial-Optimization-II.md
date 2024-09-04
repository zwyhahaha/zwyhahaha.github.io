---
layout:     post
title:      Polynomial Optimization II
subtitle:   Multivariant problems
date:       2024-09-04
author:     Wanyu Zhang
header-img: img/post-bg-rwd.jpg
catalog: 	 true
tags:
    - Polynomial Optimization
    - Optimization

---



This note is taken from the [summer course](https://sites.google.com/site/cedricjosz/home/introduction-to-polynomial-optimization), in which Prof.Cédric Josz makes everything clear and intuitive! This blog is about the multivariate polynomial optimization, including both unconstrained and constrained cases.

## Moment Approach

First, we focus on the Lasserre hierarchy for GLOBAL polynomial optimization

> ”Global Optimization with Polynomials and the problem of moments”, by Jean B. Lasserre (2001)

To get some intuition of moment approach, we transform optimization problem over a set of points into the ones over a set of measures. To be specific, a polynomial optimization problem


$$
\inf_{x \in \mathbb{R}^n} f(x) \quad \text{s.t.} \quad x\in K:=\{x \in \mathbb{R}^n|g_i(x) \geq 0, i=1,...,m\}
$$


is equivalent to the convex problem


$$
\inf_{\mu \in \mathcal M(K)}\quad \int f \text{d} \mu\\
\text{s.t.} \quad \int 1 \text{d} \mu =1 ,\mu \geq 0
$$


where $\mathcal M(K)$ denotes the set of finite Borel measures on $K$. Let $x^{\star}=\arg\min_{x\in K} f(x)$ , then $\mu^{\star}=\delta_{x^{\star}}$ is the optimal solution of (2).

### Unconstrained Case

For unconstrained multivariant polynomial optimization problem $\min_x \sum_{\alpha} p_{\alpha} x^{\alpha}$, the moment method solves


$$
P=\min_y \sum_{\alpha} p_{\alpha} y_{\alpha}\\
\text{s.t.}\quad y_{\alpha}=\int x^{\alpha} \text{d} \mu
$$




