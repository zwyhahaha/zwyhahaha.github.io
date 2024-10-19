---
layout:     post
title:      AI for Optimization Algorithms and Theories
subtitle:   
date:       2024-10-20
author:     Wanyu Zhang
header-img: img/post-bg-rwd.jpg
catalog: 	 true
tags:
    - AI
    - Optimization
---



This is the first conference day of ORSC (Operations Research Society of China) 2024, and I am impressed by the keynote talk given by Prof. Zaiwen Wen (Peking University). That's why I write this blog and share some interesting points in it.

The talk is mainly about "AI for Optimization Algorithms and Theories". To be specific, AI has the ability to get involved in various processes in optimization, including problem modeling, problem solving, and proof assistance. 

For mathemetical modeling, which requires to convert the complex real-world instances into concrete optimization problems. There is a stream of works, including OptiMUS (Stanford), ORLM (Cardinal Operations), and OptLLM (DAMO Academy). In my view, modeling is a downstream task of LLMs, with emphasis on supervised fine-tuning. Therefore, the main challenge is to create large-scale dataset, which is labor-intensive because the training pairs of natural language and optimization problems are scarce.

Then Prof. Wen mentioned a few of his works on applying AI to solve optimization problem, particularly the large-scaled ones. 

1. [Monte Carlo Policy Gradient Method for Binary Optimization](https://arxiv.org/abs/2307.00783)
2. [ODE-based Learning to Optimize](https://arxiv.org/abs/2406.02006)

Finally, and personally the most interesting point, is computer-aided proof, especially for theories in optimization. I often find that some proofs in OR is highly non-trivial and are generally hard for the majority. I can hardly believe that computers can even do better than us in this recognized hard problem, since machines are perceived as inable to think. In this talk, I knowed that a programming language named lean can do this! I cannot wait to try it!