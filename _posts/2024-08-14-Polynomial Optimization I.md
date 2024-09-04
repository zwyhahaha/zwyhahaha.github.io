---
layout:     post
title:      Polynomial Optimization I
subtitle:   
date:       2024-08-14
author:     Wanyu Zhang
header-img: img/post-bg-rwd.jpg
catalog: 	 true
tags:
    - Polynomial Optimization
    - Optimization
---



This note is taken from the [summer course](https://sites.google.com/site/cedricjosz/home/introduction-to-polynomial-optimization), in which Prof.Cédric Josz makes everything clear and intuitive! This blog is about univariate unconstrained polynomial optimization, and multivariate case is delayed to the next episode. 

To begin with, the univariate unconstrained polynomial optimization tackles


$$
\min_{x\in R }f(x)
$$


where $f$ is a polymonial with even degree. For example, 


$$
f(x)=\frac{1}{4}x^4+\frac{1}{8}x^3-2x^2-\frac{3}{2}x+7
$$


## Lift and Project

For the above example, we can introduce new variables

$$
\min_x f(x) =\frac{1}{4}y_4+\frac{1}{8}y_3-2y_2-\frac{3}{2}y_1+7y_0\\
\text{s.t.}  y_4 = x^4\\
  y_3 = x^3\\
  y_2 = x^2\\
  y_1 = x^1\\
  y_0 = 1
$$

For $y_0,y_1,y_2,y_3,y_4$ satisfying the constraints, we have

$$
\begin{bmatrix} y_0, y_1, y_2\\
y_1,y_2,y_3\\
y_2,y_3,y_4
\end{bmatrix}=\begin{bmatrix}1 \\x\\x^2\end{bmatrix}^T \begin{bmatrix}1 \\x\\x^2\end{bmatrix}\succeq 0
$$

Thus we can reformulate problem (3)

$$
\min_x  f(x) =\frac{1}{4}y_4+\frac{1}{8}y_3-2y_2-\frac{3}{2}y_1+7y_0\\
\text{s.t.}   y_0 = 1\\
  \begin{bmatrix} y_0, y_1, y_2\\
y_1,y_2,y_3\\
y_2,y_3,y_4
\end{bmatrix}\succeq 0
$$

The next proposition shows that the above "relaxation" is actually tight.

***Proposition 1***

The global infimum of an even-ordered polynomial, i.e.

$$
\inf_x f_{2d}x^{2d}+...+f_2 x^2+f_1x+f_0
$$

is equal to the optimal value of the convex problem


$$
\inf_x  f_{2d}x^{2d}+...+f_2 x^2+f_1x+f_0\\
\text{s.t.}  y_0=1\\
  (y_{i+j})_{0\leq i,j\leq d}\succeq 0
$$

## Sum-of-Squares

Another method is to approach the optimal value of (2) by constructing an increasing sequence of lower bounds. To be specific, we formulate (2) as a problem of maximizing the lower bound:


$$
\sup_{\lambda} \lambda\\
\frac{1}{4}x^4+\frac{1}{8}x^3-2x^2-\frac{3}{2}x+7-\lambda \geq 0, \forall x
$$


The constraint describes a set of non-negative polynomials. For non-negative univariant even order polynomials, they can always be expressed by sums of squares with the form $\sum_k p_k(x)^2$.

To optimize over this set, we write the polynomial $p(x)=\sum_{k=1}^{2d} p_k x^k$ by the quadratic form


$$
p(x)=\sum_{i,j\leq d} m_{ij} x^{i+j}=\begin{bmatrix}x_0\\.\\.\\x_d \end{bmatrix}^T \begin{bmatrix}m_{00}, ..., m_{0d}\\...\\...\\m_{d0}, ..., m_{dd} \end{bmatrix} \begin{bmatrix}x_0\\.\\.\\x_d \end{bmatrix}
$$


If $p(x)$ is a non-negative polynomial, the quadratic form also has an important property:

***Proposition 2*** (informal)

>  $p$ is a sum-of-squares if and only if there is at least one matrix representation that is positive semidefinite.



To see how the algorithm works, we go back to the example (2). It is now reformulated as


$$
\sup_{\lambda} \lambda\\
\frac{1}{4}x^4+\frac{1}{8}x^3-2x^2-\frac{3}{2}x+7-\lambda = \sum_{0\leq i,j\leq 2} m_{ij} x^{i+j}\\
(m_{ij})_{0\leq i,j\leq 2} \succeq 0
$$


By equating the coefficients,


$$
\sup_{\lambda} \lambda\\
7-\lambda=m_{00}\\
-\frac{3}{2}=m_{10}+m_{01}\\
-2=m_{20}+m_{11}+m_{02}\\
\frac{1}{8}=m_{21}+m{12}\\
\frac{1}{4}=m_{22}\\
(m_{ij})_{0\leq i,j\leq 2} \succeq 0
$$


In the end, we remark that the `sum-of-squares` approach is the dual of  `lift and project` approach and strong duality holds. However, the multivariant case is quite different, see the next post!
