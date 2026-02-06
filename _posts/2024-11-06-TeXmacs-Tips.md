---
layout:     post
title:      TeXmacs Tips
subtitle:   Efficient Math Typing, Crash Fixes, and More
date:       2024-11-06
author:     Wanyu Zhang
header-img: img/home-bg-o.jpg
catalog: 	 true
tags:
    - Tips
---

## About TeXmacs

[TeXmacs](https://www.texmacs.org/tmweb/home/welcome.en.html) is my favorite text editor, especially useful for those who frequently need to type mathematical formulas. I highly recommend giving it a try!

In case you need help getting started, here are some tutorials that might be useful:

- [https://www.texmacs.org/tmweb/home/videos.en.html](https://www.texmacs.org/tmweb/home/videos.en.html)
- [https://whzecomjm.com/p/2021/04/texmacs/](https://whzecomjm.com/p/2021/04/texmacs/)
- [https://x-wei.github.io/soft/TeXmacs_intro.html](https://x-wei.github.io/soft/TeXmacs_intro.html)

Hope you enjoy using TeXmacs! :) I will keep updating this post whenever I find new tips!

## Math typing tips

- Use `option F` to create fraction numbers.

- Type `shift [ + Tab` to create various brackets, which is much more convenient than `\langle \rangle`.

- Select some content and type `\red` to mark it in red, which is faster than selecting color in the menu.

- :star: **How to define Assumption environment or other theorem-like environment?**

  Enter the preamble (Select `Document->Part->Show preamble`), and type

  ```scheme
  <new-theorem|assumption|Assumption>
  ```

  Then return to the file and type `\assumption` to define assumptions! Here are the references:

  http://forum.texmacs.cn/t/how-do-i-add-a-new-environment-assumption/795/2

  https://www.texmacs.org/tmdoc/main/styles/env/env-base-dtd.en.html

- :crystal_ball: **Magic `right click`: Customized environment**

  In the `Algorithm` environment, `right click->Preferences->Framed Programs` to add box on your algorithm block. Also, you can selected `named` environment. There are so many customized functions by `right click`. Also, in the `theorem` environment, you can `right click->Preferences->European Numbering Style` to seperately number the lemmas, theorems, etc.

  In the bibliography macro, right click and you can rename the sections as `References`.

- Insert multiple citations: [Here](https://lists.texmacs.org/wws/arc/texmacs-users/2023-02/msg00015.html?utm_source=chatgpt.com) is the source of solution. 

  In the \cite macro, after inserting one citation, click on the right arrow  in the focus bar, and you will see one more argument for the second citation term. This is like adding columns in a table.

## How to fix TeXmacs crash

Recently, I encountered a TeXmacs crash on my MacBook, which was quite frustrating since I couldn’t use it for note-taking. :( Here is a guide to help you fix it. The crash is likely caused by a full cache, and clearing it should resolve the issue.

For macOS and Linux, run:

```bash
rm -fr ~/.TeXmacs
```

For Windows, the cache is located at `%APPDATA%\TeXmacs` and `C:\Users\[User name]\AppData\Roaming\TeXmacs`.

## TeXmacs to MarkDown

Since I occasionally write blog posts, I need a way to convert `.tm` files to `.md` files. Unfortunately, this feature is not available in the default TeXmacs installation, so you'll need to install additional plugins.

Here is a repository for the `tm2md` converter: [tm2md GitHub Repo](https://github.com/PikachuHy/texmacs-converter-tm2md)

For macOS:

```bash
mkdir -p ~/.TeXmacs/progs/convert
cd ~/.TeXmacs/progs/convert
git clone git@github.com:PikachuHy/texmacs-converter-tm2md.git markdown
```

open `~/.TeXmacs/progs/my-init-texmacs.scm`, and add the following code

```scheme
(use-modules (convert markdown init-markdown))
```

For Windows, refer to the repository instructions for setup details.

