---
layout:     post
title:      Equivalence of PDHG and DRS
subtitle:   
date:       2024-08-02
author:     Wanyu Zhang
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - PDHG
    - DRS
---

The PDHG algorithm solves the following composite optimization problem:

$$
\min_x f (x) + g (A x)
$$

where $x \in \mathbb{R}^n, A \in \mathbb{R}^{m \times n}$, and $f, g$ are convex closed functions with nonempty domains.

## PDHG

The primal-dual formulation of this problem is:

$$
\min_x \max_{\lambda} L (x, \lambda) = f (x) - \lambda^T A x - g^{\ast}
  (\lambda)
$$

Starting from point $(x^k, \lambda^k)$, the PDHG iteration is:

$$
x^{k + 1} = & \text{argmin}_x \left\{ f (x) - \langle A^T \lambda^k, x - x^k
  \rangle + \frac{1}{2 t} \| x - x^k \|_2^2 \right\} = \text{prox}_{t f} (x^k - t A^T \lambda^k) \\
  
\lambda^{k + 1} = & \text{argmin}_{\lambda} \left\{ g^{\ast} (\lambda) + \langle A^T (2 x^{k + 1} - x^k), \lambda - \lambda^k \rangle + \frac{t}{2} \| \lambda - \lambda^k \|_2^2 \right\} = \text{prox}_{t^{- 1} g^{\ast}} \left( \lambda^k + \frac{1}{t} A (2 x^{k + 1} - x^k) \right) 
$$

In the language of operator theory, the update rule is:

$$
  x^{k + 1} = & J_{t F} (x^k - t A^T \lambda^k) \\
  \lambda^{k + 1} = & J_{t^{- 1} G^{\ast}} \left( \lambda^k + \frac{1}{t} A (2x^{k + 1} - x^k) \right) 
$$

where $F, G^{\ast}$ are the subgradients of $f, g^{\ast}$, which are maximal monotone, and $J_F, J_{G^{\ast}}$ are their resolvents. Next, we will transform the PDHG iteration into DRS.

First, we assume that $A A^T = I$. In the later section, we would show that any problem can be transformed to satisfy this condition. Let $y^k = x^k - t
A^T \lambda^k$:

$$
  x^{k + 1} = & J_{t F} (y^k) \nonumber\\
  \lambda^{k + 1} = & J_{t^{- 1} G^{\ast}} \left( \lambda^k + \frac{1}{t} A (2
  x^{k + 1} - (t A^T \lambda^k + y^k)) \right) = J_{t^{- 1} G^{\ast}} \left(
  \frac{1}{t} A (2 x^{k + 1} - y^k) \right) \nonumber
$$

Next we apply the property of inverse operators, which states that

$$
J_{\lambda F} + \lambda J_{\lambda^{- 1} F^{- 1}} (x / \lambda) =  x
  \nonumber
$$

Thus the dual iteration reduces to

$$
\lambda^{k + 1} =  \frac{1}{t} [A (2 x^{k + 1} - y^k) - J_{t G} (A (2 x^{k+1} - y^k))] \nonumber
$$

Lastly, substituting $x^{k + 1}, \lambda^{k + 1}$ in the definition of $y^{k +1}$:

$$
y^{k + 1} = & x^{k + 1} - t A^T \lambda^{k + 1} \nonumber\\
\lambda^{k + 1}  = & x^{k + 1} - A^T A (2 x^{k + 1} - y^k) + A^T J_{t G} (A (2 x^{k + 1} -
  y^k)) \nonumber
$$

So PDHG iteration on $(x, \lambda)$ can be viewed as fixed point iteration on $y = x - t A^T \lambda$, where

$$
T (y) = J_{t F} (y) - A^T A (2 J_{t F} (y) - y) + A^T J_{t G} (A (2 J_{t
  F} (y) - y)) \nonumber
$$

## DRS

DRS aims to find $y$, such that

$$
  0 \in  \partial f (y) + A^T \partial g (A y) \nonumber
$$

Then we denote operators $\partial f, A^T \partial g A$ by $F, H$. Starting from $y^k$, DRS iteration gives

$$
  w^{k + 1} = J_{t F} (y^k) \nonumber \\
  v^{k + 1} = J_{t H} (2 w^{k + 1} - y^k) \nonumber \\
  y^{k + 1} = y^k - w^{k + 1} + v^{k + 1} \nonumber 
$$

By the property of composite operators, when $A A^T = I$ and $H = A^T G A$

$$
  J_H (x) =  (I - A^T A) x + A^T J_G (A x) \nonumber
$$

Plugging this into the update of $v$

$$
v^{k + 1} = & (I - A^T A) (2 w^{k + 1} - y^k) + A^T J_{t G} (A (2 w^{k + 1}-y^k)) \nonumber\\
y^{k + 1} = & w^{k + 1} - A^T A (2 w^{k + 1} - y^k) + A^T J_{t G} (A (2 w^{k+1} - y^k)) \nonumber
$$

Finally, the DRS can be represented by the fixed point iteration:

$$
y^{k + 1} =  J_{t F} (y^k) - A^T A (2 J_{t F} (y^k) - y^k) + A^T J_{t G} (A
  (2 J_{t F} (y^k) - y^k)) \nonumber
$$

which is the same as PDHG.

**remark**
  If the assumption $A A^T = I$ not hold, choose $\gamma \| A \| \leq 1$, we can construct the following matrix:
  
$$
B = \left[ A \quad C \right], C = (\gamma^{- 2} I - A A^T)^{1 / 2} \in
     \mathbb{R}^{m \times m}
$$

 such that $B B^T = \gamma^{- 2} I$. Then we consider the following optimization problem
 
$$
    \min_{x, u}  f (x) +\mathbb{I} (u = 0) + g (B [x, u]^T) \nonumber
$$

  whose optimal solution of variable $x$ is the same as the previous one, and $u^{\ast} = 0$.
