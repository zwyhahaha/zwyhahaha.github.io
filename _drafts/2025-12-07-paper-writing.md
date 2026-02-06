---
layout:     post
title:      Non-Universal Tips for Paper Writing
subtitle:   
date:       2025-12-07
author:     Wanyu Zhang
header-img: img/home-bg.jpg
catalog: 	 true
tags:
    - Tips
---

I am writing my first first-author paper recently. As a freshman in paper-writing, I logged some tips that I learned from exsting research papers and my co-authors. Hopefully, this would be helpful for those who are also struggling with their first papers (in optimization).

- Accompany each math notation by its meaning, like 'condition number $\kappa$'.

- Denote algorithms. If the name of the algorithm is XYZ. After defining the name, use XYZ throughout the paper. If the algorithm is also presented in a pseudocode Algorithm 1, use a link to indicate its location, 'the pseudocode of XYZ is presented in Algorithm 1'. Afterwards, still use XYZ to denote the algorithm, instead of Algorithm 1.

- Do not abuse 'we'. Only use it when, 'we developed the algorithm'. Sometimes, the subject is the algorithm, or the theorem.

- Use 'Lemma' for introductory analysis tools. Use 'Proposition' for important, interesting results which are secondary to the main theorem. Use 'Theorem' for the main contribution of the paper. Use 'Corollary' for derivative results.

- Overleaf Github Sync: 

- git pull   # get latest

  \# edit locally

  git commit -am "..."

  git push   # GitHub ↔ Overleaf integration keeps them in sync