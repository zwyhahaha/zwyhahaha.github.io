---
layout:     post
title:      Performance Estimation Problems II
subtitle:   Convergence Proofs and Stepsize Optimization
date:       2024-11-05
author:     Wanyu Zhang
header-img: img/post-bg-coffee.jpeg
catalog: 	 true
tags:
    - Optimization
    - Performance Estimation Problems
---

This is the second post in a series on **Performance Estimation Problems (PEP)**. In this post, I’ll introduce applications of the PEP framework, particularly in convergence proofs and stepsize optimization.

## Recap

Let's briefly review the basics of PEP framework $(\mathcal{P}, \mathcal{F}, \mathcal{I}, \mathcal{M})$:

- Realize by $ f (x_N) - f_{*}, \mathcal{F}_{0, L}, \| x_0 - x_{\star} 
  \| \leq R,˙x_i = x_{i - 1} - \frac{h}{L} f (x_{i - 1}) $
- Interpolation: $f \in \mathcal{F} \longrightarrow \{ x_i, f_i, g_i \}$, and interpolation conditions
- Reformulate into SDP

Given stepsize $h$, and total iteration number $N$, we can estimate the exact worst-case performance $\mathcal{P}$ of first-order method 
$\mathcal{M}$ on function class $\mathcal{F}$.

## Convergence Proofs

The primary goal of PEP is to provide multi-step convergence proofs, either analytically or numerically. Specifically,

- When a closed-form solution of the final SDP is available, the worst-case performance is characterized analytically.
- If the solution is non-trivial, the worst-case performance can also be chatacterized numerically.

Let's start from the most simple case: gradient descent (constant stepsize) on convex smooth functions. For this setting, the textbook result is


$$
f (x_N) - f (x_{\star}) \leq \frac{L \| x_0 - x_{\star} \|^2}{2 N}
$$



whereas Drori and Teboulle (2014) [1] showed that the convergence rate given by PEP is


$$
f (x_N) - f (x_{\star}) \leq \frac{L \| x_0 - x_{\star} \|^2}{4 N h + 2}
$$


where $h$ is the constant stepsize. This bound is tighter than the textbook result, and is shown to be optimal. Here’s an outline of their proof:

* Find a feasible dual SDP solution (in analytical form and depends on $N$), and the dual objective value is the upper bound of the worst-case performance.
* Find a convex function $\varphi$, and show that $\varphi (x_N) - 
  \varphi_{\star}$ is exactly $\frac{L R^2}{4 N h + 2}$.

For other first-order methods, like heavy-ball method (HBM) and fast gradient descent (FGM), the analytical bound is difficult, but  a numerical bound can be calculated by solving PEP for each $N$.

## Stepsize Optimization

The idea of using PEP to optimize stepsize is straightforward:

*  PEP: given stepsize, and define $(\mathcal{P}, \mathcal{F}, \mathcal{I}, 
   \mathcal{M})$, we can analyze the worst-case performance.
*  The stepsize can be chosen to optimze the worst-case performance.
*  Define a minimax problem: outer is stepsize optimization, inter is worst-case estimation.

In [1], Drori and Teboulle choose optimal stepsize for FGD, the main technical challenge is to relax and simplify the minmax problem to make it tractable. Their reformulation roadmap is as follows:

* Convert the inner maximization SDP into a dual minimization SDP.
* Combine with the outer minimization to form a joint minimization problem.
* Relax the resulting bilinear problem into a linear SDP for tractability.

While PEP improvements thus far have primarily impacted constant factors, Grimmer has shown that PEP-based approaches can achieve an improved rate. Below is a summary of these results, mainly on the gradient descent algorithm with long steps:

- In [2], a *straightforward* stepsize pattern $h$ is defined is shown to converge

  
  $$
  f (x_T) - f (x_{*}) \leq \frac{L
     R^2}{{{{\operatorname{avg}} (h)}} T} + O (
     \frac{1}{T^2})
  $$

  

  and they conjecture that ${\operatorname{avg}} (h) = \Omega (\log T)$.

- In [3], they proved that by using *nonconstant, nonperiodic* stepsize,

  

$$
\min_i f (x_i) - f (x_{*}) \leq \frac{11.7816 L
   R^2}{{T^{1.0564}}}
$$



## References

[1] Drori, Yoel, and Marc Teboulle. ‘‘Performance of first-order methods for smooth convex minimization: a novel approach."*Mathematical Programming*145.1 (2014): 451-482.

[2] Grimmer, Benjamin. ‘‘Provably faster gradient descent via long steps."*SIAM Journal on Optimization*34.3 (2024): 2588-2608.

[3] Grimmer, Benjamin, Kevin Shu, and Alex L. Wang. ‘‘Accelerated gradient descent via long steps."*arXiv preprint arXiv:2309.09961*(2023).