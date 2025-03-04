---
layout:     post
title:      A Simple Proof for the Nonexpansiveness and Contraction Properties of PDHG
subtitle:   
date:       2025-03-04
author:     Wanyu Zhang
header-img: img/post-bg-coffee.jpeg
catalog: 	 true
tags:
    - Optimization
---

In this blog, we introduce how to simply derive the nonexpansiveness and contraction properties of primal-dual hybrid gradient method (PDHG) iteration through the language of operator theory.

In [1], Lu and Yang introduced a unified iteration form of proximal point method, PDHG, and ADMM:

$$
P (z - z_A) \in \mathcal{F} (z_A)
$$

$z_A$ is the next iteration, $\mathcal{F}$ is a subdifferential operator, $P$ is a positive semi-definite iteration matrix and varies between different algorithms. 

## Assumptions

**1. Motononicity** Consider the property of $\mathcal{F}$. When $F$ is convex, $\mathcal{F}$ is maximal monotone, which implies that


$$
\langle z_1 - z_2, f_1 - f_2 \rangle \geq 0, \quad f_1 \in \mathcal{F} (z_1), f_2 \in
   \mathcal{F} (z_2)
$$


Apply this property on point $z_A$ and $z_{\star}$, then


$$
\langle P (z - z_A) - P (z_{\star} - z_{\star}), (z_A - z_{\star}) \rangle
   \geq 0
$$



simplify it,


$$
\langle z - z_A, z_A - z_{\star} \rangle_P \geq 0 \quad (1)
$$



**2. Sharpness** [2] has shown a definition of sharpness condition:


$$
\alpha^2 \| z - z_{\star} \|^2_P \leq \| z - z_A \|^2_P  \quad (2)
$$


## Proof

### Nonexpansiveness

First we prove monotonicity of distance to optimality using (1).

$$
{\color{red}{\| z - z_{\star} \|_P^2}} = \| z - z_A \|_P^2 + \| z_A -
  z_{\star} \|_P^2 + 2 \langle z - z_A, z_A - z_{\star} \rangle_P
  {\color{red}{\geq \| z_A - z_{\star} \|_P^2}}
$$

### Contraction

Then we prove contraction using (1) and (2). Let


$$
\rho = \frac{\| z_A - z_{\star} \|^2_P}{\| z - z_{\star} \|^2_P}
$$


WLOG, fix $\| z - z_{\star} \|^2_P = 1$.

$$
\| z - z_A \|_P^2 + \| z_A - z_{\star} \|_P^2 \leq
   {\| z - z_{\star} \|_P^2} \leq
   \frac{1}{\alpha^2} \| z - z_A \|^2_P \quad \Rightarrow \quad
   \frac{\alpha^2}{1 - \alpha^2} \| z_A - z_{\star} \|_P^2 \leq \| z - z_A \|^2_P
$$

$$
\frac{\alpha^2}{1 - \alpha^2} \| z_A - z_{\star} \|_P^2 + \| z_A -
   z_{\star} \|_P^2 \leq \| z - z_A \|^2_P + \| z_A - z_{\star} \|_P^2 \leq \|
   z - z_{\star} \|^2_P = 1
$$

Finally,

$$
 {\color{red}{\rho}} = \| z_A - z_{\star} \|_P^2 {\color{red}{\leq 1 -
   \alpha^2}} 
$$

## References

[1] Lu, Haihao, and Jinwen Yang. ‘‘On a unified and simplified proof for the ergodic convergence rates of ppm, pdhg and admm.*arXiv preprint arXiv:2305.02165*(2023).

[2] Lu, Haihao, and Jinwen Yang. ‘‘Restarted Halpern PDHG for linear programming."*arXiv preprint arXiv:2407.16144*(2024).

