---
layout:     post
title:      Life Lessons from Optimization
subtitle:   
date:       2024-12-10
author:     Wanyu Zhang
header-img: img/home-bg-o.jpg
catalog: 	 true
tags:
    - Optimization

---

As shown in the title, maybe it sounds wiered to link optimization with "life lessons", but it comes true at Prof. Yinyu Ye's courses at SJTU. I am deeply impressed by these ideas and insights, and I believe some of them is not limited to the field of optimization, but to other fields like computer science, even our lives.

The first lesson is to **decompose a difficult task into smaller or easier ones**. This is drawned from the path-following algorithm. Facing the challenging goal of quickly finding the optimal solution of a convex (but not strongly-convex) function, it is better to break it into easier strongly-convex subproblems, such that Newton method has a quadratic convergence in each subproblem. I have seen similar insights in generative models. It is hard to generate a sentense or a clear image *at once*, but it is much simpler to generate the next word or slightly cleaner image given the current states, and this is how transformers and diffusion models work. 

The second lesson is that **randomization helps**. This is drawn from the ADMM algorithm, where the parameters are divided into several blocks and updated in a Gauss-Seidel type. Prof. Ye points out that if we fix the updating order, ADMM may diverge in the 3-block case. However, the convergence can be guaranteed if the updating rule is randomly permuted in each iteration. I think this idea is widely used in practice, where people set `shuffle=True` in DataLoader. Broaderly, in the context of online learning algorithms, we know that random algorithms have better competitive ratio than deterministic ones, like the randomized marking algorithm in caching. 

There are few advices on doing research.

Prof. Ye stresses the importance of math. He showed a demo of SDP relaxation on sensor network localization problem, where some sensors are accurately identified but others not. What impressed me is that Prof. Ye can explain the successes and failures clearly, and actually he has a theory of rigility on that. It is all about the thorough understanding of the problem and everything becomes explainable and within the control. I have done many experiments, and it is common to see unexpected and unexplainable results. It is time to stop and think about why. As Prof. Ye said, in the era of LLM, the meaning of math optimization is to identify the efficient and theoretically guaranteed algorithms.