---
layout:     post
title:      Envelope Function for Extended DRS
subtitle:
date:       2026-06-10
author:     Wanyu Zhang
header-img: 
catalog:    true
tags:
    - Optimization
---

Operator splitting methods, like forward backward splitting (FBS) and Douglas-Rachford splitting (DRS), can be viewed as gradient descent on the envelope function. This point of view is useful because it turns a nonsmooth splitting iteration into a smooth optimization method on a surrogate objective. Related envelope constructions also appear for other splitting schemes, such as the [Davis-Yin envelope](https://arxiv.org/abs/1804.08739).

In this post I first review the classical envelope functions for FBS and DRS, and then derive the corresponding envelope for **extended DRS**. Throughout, I write the composite objective as

$$
F(u):=f(u)+g(u),
$$

where $f$ is the smooth block and $g$ is the prox-friendly, possibly nonsmooth block. For DRS, I also assume that the proximal map of $f$ is tractable.

## 1. Envelope functions for FBS and DRS

**FBS.** Suppose $f$ is convex, twice differentiable, and $L_f$-smooth, and $g$ is proper, closed, convex, and proximable. The FBS step with stepsize $\gamma>0$ is

$$
x^+ = \operatorname{prox}_{\gamma g}\bigl(x-\gamma \nabla f(x)\bigr).
$$

The **forward-backward envelope** (FBE), introduced by [Patrinos, Stella, and Bemporad](https://arxiv.org/abs/1402.6655), is

$$
F_\gamma^{\mathrm{FB}}(x)
:=
f(x)-\tfrac{\gamma}{2}\|\nabla f(x)\|^2
+g_\gamma\bigl(x-\gamma\nabla f(x)\bigr),
$$

where $g_\gamma$ is the Moreau envelope of $g$. Then FBS can be written as a variable-metric gradient step on the FBE:

$$
x^+
=
x-\gamma\bigl(I-\gamma\nabla^2 f(x)\bigr)^{-1}
\nabla F_\gamma^{\mathrm{FB}}(x).
$$

When $0<\gamma<1/L_f$, the envelope is exact:

$$
\min_x F(x)=\min_x F_\gamma^{\mathrm{FB}}(x),
\qquad
\operatorname{argmin} F
=
\operatorname{argmin} F_\gamma^{\mathrm{FB}}.
$$

So minimizing the FBE is equivalent to solving the original composite problem, but the FBE is differentiable even when $g$ is nonsmooth.

**DRS.** To obtain a smooth envelope, assume that $f$ is twice differentiable and $L_f$-smooth. Define

$$
P_\gamma(x):=\operatorname{prox}_{\gamma f}(x),
\qquad
G_\gamma(x):=\operatorname{prox}_{\gamma g}\bigl(2P_\gamma(x)-x\bigr).
$$

The classical DRS step is

$$
x^+=x+G_\gamma(x)-P_\gamma(x).
$$

The **Douglas-Rachford envelope** (DRE), introduced by [Patrinos, Stella, and Bemporad](https://arxiv.org/abs/1407.6723), is

$$
F_\gamma^{\mathrm{DR}}(x)
:=
f_\gamma(x)-\gamma\|\nabla f_\gamma(x)\|^2
+g_\gamma\bigl(x-2\gamma\nabla f_\gamma(x)\bigr).
$$

DRS is again a variable-metric gradient method:

$$
x^+
=
x-\gamma
\bigl(I-2\gamma\nabla^2 f_\gamma(x)\bigr)^{-1}
\nabla F_\gamma^{\mathrm{DR}}(x).
$$

When $0<\gamma<1/L_f$, the DRE is exact up to the proximal map $P_\gamma$:

$$
\min_u F(u)=\min_x F_\gamma^{\mathrm{DR}}(x),
\qquad
P_\gamma\bigl(\operatorname{argmin}F_\gamma^{\mathrm{DR}}\bigr)
=
\operatorname{argmin}F.
$$


## 2. Extended DRS

A recent paper by [Nilsson, Åkerman, and Giselsson](https://arxiv.org/abs/2511.19637) studies an extended DRS family with two proximal stepsizes. For the optimization problem

$$
\min_u F(u),
$$

extended DRS takes the form

$$
P_\alpha(x):=\operatorname{prox}_{\alpha f}(x),
$$

$$
G_{\alpha,\beta}(x)
:=
\operatorname{prox}_{\beta g}
\left(
\left(1+\tfrac{\beta}{\alpha}\right)P_\alpha(x)
-
\tfrac{\beta}{\alpha}x
\right),
$$

$$
x^+
=
x+\theta\bigl(G_{\alpha,\beta}(x)-P_\alpha(x)\bigr).
$$

The standard DRS iteration is recovered by setting $\alpha=\beta=\gamma$ and $\theta=1$. For the convex optimization setting, [the extended DRS paper](https://arxiv.org/abs/2511.19637) gives the convergence range

$$
0<\theta<\min\left\{2,\tfrac{2\alpha}{\beta}\right\}.
$$

## 3. Extended Douglas-Rachford envelope

The extended DRS envelope is

$$
F_{\alpha,\beta}^{\mathrm{EDR}}(x)
:=
f_\alpha(x)
-
\tfrac{\alpha+\beta}{2}\|\nabla f_\alpha(x)\|^2
+
g_\beta\bigl(x-(\alpha+\beta)\nabla f_\alpha(x)\bigr).
$$

The key identity is

$$
x-(\alpha+\beta)\nabla f_\alpha(x)
=
\left(1+\tfrac{\beta}{\alpha}\right)P_\alpha(x)
-
\tfrac{\beta}{\alpha}x.
$$

Therefore the last term in $F_{\alpha,\beta}^{\mathrm{EDR}}$ is exactly the Moreau envelope associated with the second proximal step in extended DRS.

Hence the extended DRS update can be written as

$$
x^+
=
x-\theta\beta
\bigl(I-(\alpha+\beta)\nabla^2 f_\alpha(x)\bigr)^{-1}
\nabla F_{\alpha,\beta}^{\mathrm{EDR}}(x),
$$

whenever $0<\beta<1/L_f$. Thus extended DRS is gradient descent on the extended DRE, under a variable metric.

**Exactness of the extended envelope.** The same envelope sandwich argument extends to $F_{\alpha,\beta}^{\mathrm{EDR}}$. For $P=P_\alpha(x)$, $G=G_{\alpha,\beta}(x)$, and $R=P-G$, we have

$$
F(G)
+
\tfrac{1-\beta L_f}{2\beta}\|R\|^2
\le
F_{\alpha,\beta}^{\mathrm{EDR}}(x)
\le
F(P)
-
\tfrac{1}{2\beta}\|R\|^2.
$$

Therefore, if $0<\beta<1/L_f$ and the original problem has a minimizer, then

$$
\min_x F_{\alpha,\beta}^{\mathrm{EDR}}(x)
=
\min_u F(u),
\quad
P_\alpha\bigl(\operatorname{argmin}F_{\alpha,\beta}^{\mathrm{EDR}}\bigr)
=
\operatorname{argmin}F.
$$


**Convex and smooth envelope in the quadratic case.** Suppose

$$
f(u)=\tfrac{1}{2}u^\top Q u+q^\top u,\;
\mu I\preceq Q\preceq L I
$$

and $g$ is proper, closed, convex, and proximable. In this case, if $\alpha>0$ and $0<\beta\le 1/L$, then the extended DRE is smooth and convex with 

$$
L_{\alpha,\beta}^{\mathrm{EDR}}
=
\tfrac{1-\beta\mu}{\beta(1+\alpha\mu)^2},
\qquad
\mu_{\alpha,\beta}^{\mathrm{EDR}}
=
\min\left\{
\tfrac{\mu(1-\beta\mu)}{(1+\alpha\mu)^2},
\tfrac{L(1-\beta L)}{(1+\alpha L)^2}
\right\}.
$$

This gives a clean smooth convex objective on which the extended DRS iteration is simply a gradient method with a variable metric.


## References

1. Panagiotis Patrinos, Lorenzo Stella, and Alberto Bemporad. [Forward-Backward Truncated Newton Methods for Convex Composite Optimization](https://arxiv.org/abs/1402.6655), 2014.
2. Panagiotis Patrinos, Lorenzo Stella, and Alberto Bemporad. [Douglas-Rachford Splitting: Complexity Estimates and Accelerated Variants](https://arxiv.org/abs/1407.6723), 2014.
3. Max Nilsson, Anton Åkerman, and Pontus Giselsson. [Extending Douglas-Rachford Splitting for Convex Optimization](https://arxiv.org/abs/2511.19637), 2025.
4. Yanli Liu and Wotao Yin. [An Envelope for Davis-Yin Splitting and Strict Saddle Point Avoidance](https://arxiv.org/abs/1804.08739), 2019.
