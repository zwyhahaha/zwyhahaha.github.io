---
layout:     post
title:      Having Fun with Coding 🎵
subtitle:   
date:       2024-12-01
author:     Wanyu Zhang
header-img: img/home-bg-o.jpg
catalog: 	 true
tags:
    - Productivity
---

I recently got fascinated by writing code! A well-written, clearly organized, and particularly high-performing code is really like an artwork. With this mindset, coding is not just laborious work, but a creating process. Here are some tips on how to enjoy coding.

1. Choose a beautiful theme on your coding interface. This depends on the current mood. I typically choose gold or purple. Once I tried a new theme, I became more focused.
2. Keep a note in your coding process. Log some TODO lists and challenges, and address them one by one. These small positive feedbacks mean a lot when you are working on a large project.
3. Use tools for productivity. I use Copilot to assist with my coding. I do not need to bother copying and pasting the `ArgParse` function again and again, just prompt: *write a function to parse learning rate, batch size, bala bala...*
4. Search for relevant GitHub repos when you hope to implement a test environment; working on them will greatly save you time. For example, I recently worked on testing the performance of a new optimizer and found that there are already many well-established repos with comprehensive benchmarks for optimizers.
5. Switch to full-screen mode and turn off your notices. Delve into the moment and enjoy focusing.

------

Besides, I summarized some frequently used commands here, and I will keep updating them! 💨 Since I use MacOS, the commands listed below may only apply to MacOS and Linux systems.

1. `tmux` commands

   I use `tmux` windows to run and manage large experiments in case the `LSF` (Load Sharing Facility) scheduling system is not available.

   | Operation                     | Command                       |
   | ----------------------------- | ----------------------------- |
   | create a session              | `tmux new -s [Name]`          |
   | exit                          | `Ctrl+b d` or `tmux detach`   |
   | return to an existing session | `tmux a -t [Name]`            |
   | kill a session                | `tmux kill-session -t [Name]` |
   | view all sessions             | `tmux ls`                     |

2. Conda environment

   | Operation                        | Command                                 |
   | -------------------------------- | --------------------------------------- |
   | create                           | `conda create -n [EnvName] python=3.10` |
   | activate                         | `conda activate [EnvName]`              |
   | view packages under  current env | `conda list`                            |
   | view all envs                    | `conda env list`                        |
   | remove (be careful!)             | `conda env remove -n [EnvName]`         |

3. Set mirrors to accelerate downloading

   (a) PyPI

   ```bash
   mkdir -p ~/.pip
   nano ~/.pip/pip.conf
   ```

   and write

   ```yaml
   [global]
   index-url = https://pypi.tuna.tsinghua.edu.cn/simple
   ```

   and verify

   ```bash
   pip config list
   ```

   

   (b) Conda

   ```bash
   conda config --set show_channel_urls yes
   nano ~/.condarc
   ```

   and write

   ```yaml
   channels:
     - defaults
   default_channels:
     - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
     - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
   custom_channels:
     conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
   ```

   and verify

   ```bash
   conda config --show
   ```

4. 
