---
layout:     post
title:      TeXmacs Tips
subtitle:   Efficient Math Typing, Crash Fixes, and More
date:       2024-11-06
author:     Wanyu Zhang
header-img: img/home-bg-o.jpg
catalog: 	 true
tags:
    - TeXmacs
    - Productivity
---

## About TeXmacs

[TeXmacs](https://www.texmacs.org/tmweb/home/welcome.en.html) is my favorate text editor, especially useful for those who frequently need to type mathematical formulas. I highly recommend giving it a try!

In case you need help getting started, here are some tutorials that might be useful:

- [TeXmacs Video Tutorials](https://www.texmacs.org/tmweb/home/videos.en.html)
- [TeXmacs Guide by whzecomjm](https://whzecomjm.com/p/2021/04/texmacs/)
- [Introduction to TeXmacs by x-wei](https://x-wei.github.io/soft/TeXmacs_intro.html)

Hope you enjoy using TeXmacs! :)

## How to fix TeXmacs Crash

Recently, I encountered a TeXmacs crash on my MacBook Pro, which was quite frustrating since I couldn’t use it for note-taking. :(

Here is a guide to help you fix it. The crash is likely caused by a full cache, and clearing it should resolve the issue.

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

------

Finally, let me know if you’d like any more adjustments!