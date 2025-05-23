---
layout:     post
title:      Routines for Setting Up a New Server
subtitle:   
date:       2025-05-23
author:     Wanyu Zhang
header-img: img/heart.jpeg
catalog: 	 true
tags:
    - Tips

---

Lately, I’ve been running deep learning experiments across different computing clusters. Every time I switch to a new server, I have to go through a series of setup steps to get my environment ready. To avoid repeating the same work from scratch each time, I decided to document my routine here. This post mainly serves as a personal checklist, but it might also be useful to others facing similar tasks. I’ll keep it updated whenever I add new steps to the routine.

## Connect to GitHub Account

1. Generate an SSH key

   ```shell
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

2. After generating the key, display it with:

   ```shell
   cat ~/.ssh/id_ed25519.pub
   ```

3. Add the public key to GitHub.

   Navigate to **Settings > SSH and GPG keys**

   Click **"New SSH key"**, then paste the copied content

4. Testing SSH connection.

   ```shell
   ssh -T git@github.com
   ```

   If prompted, type `yes` and press Enter.

## Set Up a Conda Environment

1. Create a new environment.

   ```shell
   conda create -n myenv python=3.10
   ```

2. Use a faster pip mirror

   ```shell
   pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
   pip config set install.trusted-host pypi.tuna.tsinghua.edu.cn
   ```

## Set Up Hugging Face Mirror

```shell
export HF_ENDPOINT="https://hf-mirror.com"
echo 'export HF_ENDPOINT="https://hf-mirror.com"' >> ~/.bashrc
```

Then reload your shell:

```shell
source ~/.bashrc
```



