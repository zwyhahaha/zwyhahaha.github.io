---
layout:     post
title:      AI for Optimization Algorithms and Theories
subtitle:   
date:       2024-10-20
author:     Wanyu Zhang
header-img: img/post-bg-rwd.jpg
catalog: 	 true
tags:
    - Optimization
---



This is the first conference day of ORSC (Operations Research Society of China) 2024, and I was impressed by Prof. Zaiwen Wen (Peking University) 's keynote talk. That's why I am writing this blog and sharing some interesting points in it.

The talk is mainly about "AI for Optimization Algorithms and Theories." To be specific, AI can be involved in various optimization processes, including problem modeling, problem-solving, and proof assistance. 

For mathematical modeling, which requires converting complex real-world instances into concrete optimization problems. There is a stream of works, including OptiMUS (Stanford), ORLM (Cardinal Operations), and OptLLM (DAMO Academy). In my view, modeling is a downstream task of LLMs, emphasizing supervised fine-tuning. Therefore, the main challenge is to create a large-scale dataset, which is labor-intensive because the training pairs of natural language and optimization problems are scarce.

Then, Prof. Wen mentioned a few of his works on applying AI to solve optimization problems, particularly large-scale ones. 

1. [Monte Carlo Policy Gradient Method for Binary Optimization](https://arxiv.org/abs/2307.00783)
2. [ODE-based Learning to Optimize](https://arxiv.org/abs/2406.02006)

Finally, and personally, the most interesting point is computer-aided proof, especially for theories in optimization. I often find some proofs in OR are highly non-trivial and generally hard for the majority. I can hardly believe that computers can even do better than we do in this recognized hard problem since machines are perceived as unable to think. In this talk, I knowed that a programming language named `lean` can do this! I plan to try this out and write a blog about it. Stay tuned.