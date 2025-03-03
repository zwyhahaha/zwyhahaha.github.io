---
layout:     post
title:      On the Regret of Prescient Online Gradient Descent
subtitle:   
date:       2025-03-03
author:     Wanyu Zhang
header-img: img/post-bg-rwd.jpg
catalog: 	 true
tags:
    - Optimization
---

For optimistic online learning, the player can predict the next gradient, and the regret bound is dependent on the cumulative prediction error. In this blog, we consider an extreme case where the player can get access to the **exact** next gradient. Under this setting, the regret can be improved to $\mathcal{O} 
(1)$. The proof is adapted from **Theorem 6.20** in this note:

>  Orabona, Francesco. ‘‘A modern introduction to online learning. *arXiv preprint arXiv:1912.13213*(2019).

------

For online learning update,
$$
\begin{array}{rcl}
	&  & x_{k + 1} = x_k - \eta \nabla \ell_{k + 1} (x_{k + 1})
\end{array}
$$
where we assume $\ell_k (x)$ is convex w.r.t. $x$. For a static action $u$, we have the following regret bound,
$$
\begin{array}{rcl}
	 &  & \sum_{k = 0}^{K - 1} (\ell_k (x_k) - \ell_k (u)) \leq \frac{1}{2 \eta} \|
   x_0 - u \|^2 + \langle x_0 - u, \nabla \ell_0 (x_0) \rangle
\end{array}
$$

**Proof.**

$$
\begin{array}{rcl}
  \langle x_k - u, \nabla \ell_{k + 1} (x_{k + 1}) \rangle & = &
  \frac{1}{\eta} \langle x_k - u, x_k - x_{k + 1} \rangle\\
  & \leq & \frac{1}{2 \eta} [\| x_k - u \|^2 - \| x_{k + 1} - u \|^2 + \| x_k
  - x_{k + 1} \|^2]\\
  & \leq & \frac{1}{2 \eta} [\| x_k - u \|^2 - \| x_{k + 1} - u \|^2] +
  \langle x_k - x_{k + 1}, \nabla \ell_{k + 1} (x_{k + 1}) \rangle
\end{array}
$$

Telescope the LHS,

$$
\begin{array}{rcl}
  &  & \sum_{k = 0}^{K - 1} \langle x_k - u, \nabla \ell_{k + 1} (x_{k + 1})
  \rangle\\
  & = & \sum_{k = 0}^{K - 1} \langle x_k - u, \nabla \ell_k (x_k) \rangle +
  \sum_{k = 0}^{K - 1} \langle x_k - u, \nabla \ell_{k + 1} (x_{k + 1}) -
  \nabla \ell_k (x_k) \rangle\\
  & \geq & \sum_{k = 0}^{K - 1} (\ell_k (x_k) - \ell_k (u)) + \sum_{k = 0}^{K
  - 1} \langle x_k, \nabla \ell_{k + 1} (x_{k + 1}) - \nabla \ell_k (x_k)
  \rangle - \sum_{k = 0}^{K - 1} \langle u, \nabla \ell_{k + 1} (x_{k + 1}) -
  \nabla \ell_k (x_k) \rangle\\
  & = & \sum_{k = 0}^{K - 1} (\ell_k (x_k) - \ell_k (u)) + \sum_{k = 0}^{K -
  1} \langle x_k, \nabla \ell_{k + 1} (x_{k + 1}) - \nabla \ell_k (x_k)
  \rangle - \langle \nabla \ell_K (x_K) - \nabla \ell_0 (x_0), u \rangle
\end{array}
$$

Telescope the RHS,

$$
\begin{array}{rcl}
  &  & \frac{1}{2 \eta} [\| x_0 - u \|^2 - \| x_K - u \|^2] + \sum_{k = 0}^{K
  - 1} \langle x_k - x_{k + 1}, \nabla \ell_{k + 1} (x_{k + 1}) \rangle
\end{array}
$$

Combine LHS and RHS together,

$$
\begin{array}{rcl}
  \sum_{k = 0}^{K - 1} (\ell_k (x_k) - \ell_k (u)) & \leq & \sum_{k = 0}^{K -
  1} [- \langle x_k, \nabla \ell_{k + 1} (x_{k + 1}) - \nabla \ell_k (x_k)
  \rangle + \langle x_k - x_{k + 1}, \nabla \ell_{k + 1} (x_{k + 1})
  \rangle]\\
  &  & + \frac{1}{2 \eta} [\| x_0 - u \|^2 - \| x_K - u \|^2] + \langle
  \nabla \ell_K (x_K) - \nabla \ell_0 (x_0), u \rangle\\
  & = & \sum_{k = 0}^{K - 1} [\langle x_k, \nabla \ell_k (x_k) \rangle -
  \langle x_{k + 1}, \nabla \ell_{k + 1} (x_{k + 1}) \rangle] + \frac{1}{2
  \eta} [\| x_0 - u \|^2 - \| x_K - u \|^2]\\
  &  & + \langle \nabla \ell_K (x_K) - \nabla \ell_0 (x_0), u \rangle\\
  & \leq & \frac{1}{2 \eta} \| x_0 - u \|^2 + \langle x_0 - u, \nabla \ell_0
  (x_0) \rangle - \langle x_K - u, \nabla \ell_K (x_K) \rangle
\end{array}
$$

Since the regret from $0$ to $K - 1$ does not depend on $\nabla \ell_K (x_K)$, we set it as ${\boldsymbol{0}}$. Then we complete the proof.

Under this case, without imposing Lipschitz or smoothness assumption on online loss, we can achieve a constant regret bound.