---
layout:     post
title:      A step-by-step derivation from DRS to ADMM
subtitle:   
date:       2026-02-05
author:     Wanyu Zhang
header-img: img/post-bg-coffee.jpeg
catalog:    true
tags:
    - Optimization
---

In this note, we present a step-by-step derivation of the Alternating Direction Method of Multipliers (ADMM) from Douglas-Rachford Splitting (DRS). This derivation is adapted from the book below and fills in the intermediate steps that were skipped in the original exposition.

> Reference: [Convex Optimization: Algorithms and Complexity](https://link.springer.com/content/pdf/10.1007/978-981-16-9840-8_2), Chapter 2.

------

## Problem Setup

Consider using ADMM to solve the following linearly constrained problem:

$$
\min_{x, y} \; f(x) + g(y) \quad \text{s.t.} \; Ax + By = b
$$

The standard ADMM update consists of alternating minimization over the primal variables followed by a dual ascent step:

$$
\begin{aligned}
x^{k+1} &= \arg\min_x \left\{ f(x) + \langle v^k, Ax \rangle + \tfrac{\beta}{2} \| Ax + By^k - b \|^2 \right\} \\
y^{k+1} &= \arg\min_y \left\{ g(y) + \langle v^k, By \rangle + \tfrac{\beta}{2} \| Ax^{k+1} + By - b \|^2 \right\} \\
v^{k+1} &= v^k + \beta (Ax^{k+1} + By^{k+1} - b)
\end{aligned}
$$

Our goal in this note is to derive the ADMM update from DRS applied to a suitable reformulation of the problem. To set the stage, consider the Fenchel dual problem:

$$
\min_{\lambda} \; \underbrace{f^{\ast}(-A^{\top} \lambda) + b^{\top} \lambda}_{\varphi_1(\lambda)} + \underbrace{g^{\ast}(-B^{\top} \lambda)}_{\varphi_2(\lambda)}
$$

This is an unconstrained minimization of the sum of two convex functions $\varphi_1$ and $\varphi_2$, which is precisely the form to which DRS applies. Applying DRS to the dual problem yields the following iteration:

$$
\begin{aligned}
v^k &= \operatorname{prox}_{\beta \varphi_2}(y^k) \\
u^{k+1} &= \operatorname{prox}_{\beta \varphi_1}(2v^k - y^k) \\
y^{k+1} &= y^k + u^{k+1} - v^k
\end{aligned}
$$

## Switched DRS

To connect DRS with ADMM, we first rewrite the iteration in a more convenient form. Consider the start of the next DRS iteration:

$$
v^{k+1} = \operatorname{prox}_{\beta \varphi_2}(y^{k+1}) = \operatorname{prox}_{\beta \varphi_2}(y^k + u^{k+1} - v^k)
$$

Then consider the DRS iteration $(u^{k+1}, y^{k+1}, v^{k+1})$ and switch the order of the $y^{k+1}$ and $v^{k+1}$ updates. Since $v^{k+1}$ depends on $y^{k+1}$ only through $y^k + u^{k+1} - v^k$, which is already determined before the switch, we derive an equivalent algorithm:

$$
\begin{aligned}
u^{k+1} &= \operatorname{prox}_{\beta \varphi_1}(2v^k - y^k) \\
v^{k+1} &= \operatorname{prox}_{\beta \varphi_2}(y^k + u^{k+1} - v^k) \\
y^{k+1} &= y^k + u^{k+1} - v^k.
\end{aligned}
$$

Next, apply the change of variable $w^k := v^k - y^k$ to simplify the expressions. Substituting into each line gives:

$$
\begin{aligned}
u^{k+1} &= \operatorname{prox}_{\beta \varphi_1}(v^k + w^k) \\
v^{k+1} &= \operatorname{prox}_{\beta \varphi_2}(u^{k+1} - w^k) \\
w^{k+1} &= w^k + v^{k+1} - u^{k+1}
\end{aligned}
$$

This is the form of DRS from which we will recover the ADMM updates.

## Recovering ADMM

We now show that the switched DRS iteration above, applied to the dual problem, is equivalent to ADMM on the original primal problem.

**Step 1: optimality condition of the $u$-update.**

Consider the optimality condition of $u^{k+1} = \operatorname{prox}_{\beta \varphi_1}(v^k + w^k)$. Recalling that $\varphi_1(\lambda) := f^{\ast}(-A^{\top} \lambda) + b^{\top} \lambda$, the proximal optimality condition reads:

$$
\begin{aligned}
0 &\in \partial \varphi_1(u^{k+1}) + \tfrac{1}{\beta}(u^{k+1} - (v^k + w^k)) \\
&= -A \, \partial f^{\ast}(-A^{\top} u^{k+1}) + b + \tfrac{1}{\beta}(u^{k+1} - (v^k + w^k))
\end{aligned}
$$

Then there exists $x^{k+1} \in \partial f^{\ast}(-A^{\top} u^{k+1})$, which by the conjugate subgradient relation implies $-A^{\top} u^{k+1} \in \partial f(x^{k+1})$, such that

$$
\begin{aligned}
0 &= -Ax^{k+1} + b + \tfrac{1}{\beta}(u^{k+1} - (v^k + w^k)) \\
(\Rightarrow) \quad u^{k+1} &= v^k + w^k + \beta(Ax^{k+1} - b)
\end{aligned} \tag{1} \label{eq:u-update}
$$

By $0 \in \partial f(x^{k+1}) + A^{\top} u^{k+1}$ and $\eqref{eq:u-update}$, we obtain

$$
0 \in \partial f(x^{k+1}) + A^{\top}(v^k + w^k) + \beta A^{\top}(Ax^{k+1} - b) \tag{2} \label{eq:x-opt}
$$

**Step 2: optimality condition of the $v$-update.**

Consider the optimality condition of $v^{k+1} = \operatorname{prox}_{\beta \varphi_2}(u^{k+1} - w^k)$. Since $\varphi_2(\lambda) := g^{\ast}(-B^{\top} \lambda)$, we have

$$
\begin{aligned}
0 &\in \partial \varphi_2(v^{k+1}) + \tfrac{1}{\beta}(v^{k+1} - (u^{k+1} - w^k)) \\
&= -B \, \partial g^{\ast}(-B^{\top} v^{k+1}) + \tfrac{1}{\beta}(v^{k+1} - u^{k+1} + w^k)
\end{aligned}
$$

Then there exists $y^{k+1} \in \partial g^{\ast}(-B^{\top} v^{k+1})$, which implies $-B^{\top} v^{k+1} \in \partial g(y^{k+1})$, such that

$$
\begin{aligned}
0 &= -By^{k+1} + \tfrac{1}{\beta}(v^{k+1} - u^{k+1} + w^k) \\
(\Rightarrow) \quad v^{k+1} &= u^{k+1} - w^k + \beta B y^{k+1}
\end{aligned} \tag{3} \label{eq:v-update}
$$

From the update rule $w^{k+1} = w^k + v^{k+1} - u^{k+1}$, substituting $\eqref{eq:v-update}$ gives a useful identity:

$$
0 = -By^{k+1} + \tfrac{1}{\beta} w^{k+1} \tag{4} \label{eq:w-identity}
$$

By $0 \in \partial g(y^{k+1}) + B^{\top} v^{k+1}$ and $\eqref{eq:v-update}$, we get

$$
0 \in \partial g(y^{k+1}) + B^{\top}(u^{k+1} - w^k) + \beta B^{\top} B y^{k+1} \tag{5} \label{eq:y-opt}
$$

**Step 3: Recover ADMM updates.**

We are now ready to piece everything together. From $\eqref{eq:x-opt}$ and $\eqref{eq:w-identity}$, note that $w^k = \beta B y^k$ by applying $\eqref{eq:w-identity}$ at iteration $k$. Substituting into $\eqref{eq:x-opt}$:

$$
0 \in \partial f(x^{k+1}) + A^{\top} v^k + \beta A^{\top}(Ax^{k+1} - b + By^k),
$$

which is precisely the optimality condition of the $x$-update of ADMM:

$$
x^{k+1} = \arg\min_x \left\{ f(x) + \langle v^k, Ax \rangle + \tfrac{\beta}{2} \| Ax + By^k - b \|^2 \right\}.
$$

From $\eqref{eq:y-opt}$ and $\eqref{eq:w-identity}$, substituting $u^{k+1} - w^k + \beta B y^{k+1} = v^{k+1}$ from $\eqref{eq:v-update}$ gives:

$$
\begin{aligned}
0 &\in \partial g(y^{k+1}) + B^{\top}(u^{k+1} - w^k + \beta B y^{k+1}) \\
&= \partial g(y^{k+1}) + B^{\top}(v^k + \beta(Ax^{k+1} + By^{k+1} - b))
\end{aligned} \tag{6} \label{eq:y-admm}
$$

where the second equality follows from $\eqref{eq:u-update}$. This is exactly the optimality condition of the $y$-update of ADMM:

$$
y^{k+1} = \arg\min_y \left\{ g(y) + \langle v^k, By \rangle + \tfrac{\beta}{2} \| Ax^{k+1} + By - b \|^2 \right\}.
$$

Finally, from $\eqref{eq:v-update}$ and $\eqref{eq:y-admm}$, we recover the dual update of ADMM:

$$
\begin{aligned}
v^{k+1} &= u^{k+1} - w^k + \beta B y^{k+1} \\
&= v^k + \beta(Ax^{k+1} + By^{k+1} - b).
\end{aligned}
$$

This completes the derivation: the switched DRS applied to the Fenchel dual is equivalent to ADMM on the primal problem.
