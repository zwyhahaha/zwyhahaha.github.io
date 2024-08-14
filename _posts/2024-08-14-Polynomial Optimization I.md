---
layout:     post
title:      Polynomial Optimization I
subtitle:   
date:       2024-08-14
author:     Wanyu Zhang
header-img: img/home-bg.jpg
catalog: 	 true
tags:
    - Polynomial Optimization
    - Optimization
---



# Polynomial Optimization I

This note is taken from the [summer course](https://sites.google.com/site/cedricjosz/home/introduction-to-polynomial-optimization), which is really amazing since Prof.Cédric Josz makes everything clear and intuitive! This blog is about univariate unconstrained polynomial optimization, and multivariate case is delayed to the next episode. 

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
\min_x & f(x) =\frac{1}{4}y_4+\frac{1}{8}y_3-2y_2-\frac{3}{2}y_1+7y_0\\
\text{s.t.} & y_4 = x^4\\
 & y_3 = x^3\\
 & y_2 = x^2\\
 & y_1 = x^1\\
 & y_0 = 1\\
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
\min_x & f(x) =\frac{1}{4}y_4+\frac{1}{8}y_3-2y_2-\frac{3}{2}y_1+7y_0\\
\text{s.t.}  & y_0 = 1\\
& \begin{bmatrix} y_0, y_1, y_2\\
y_1,y_2,y_3\\
y_2,y_3,y_4
\end{bmatrix}\succeq 0
$$


The next proposition shows that the above "relaxation" is actually tight.

***Proposition***

The global infimum of an even-ordered polynomial, i.e.


$$
\inf_x f_{2d}x^{2d}+...+f_2 x^2+f_1x+f_0
$$


is equal to the optimal value of the convex problem


$$
\inf_x & f_{2d}x^{2d}+...+f_2 x^2+f_1x+f_0\\
\text{s.t.} & y_0=1\\
& (y_{i+j})_{0\leq i,j\leq d}\succeq 0
$$




