---
layout: post
title: "GLobal .gitignore"
date: 2014-02-08 18:59:08 +0200
comments: true
categories: discoveries
tags: git
---

Very useful if you need, for example, to igonre the `.idea` directory in all your projects and not add it to each project's `.gitignore` explicitly. To do so execute the following:

```
git config --global core.excludesfile "~/.gitignore"
echo ".idea" > ~/.gitignore
```

That's it. Now the global `.gitignore` will act just like the project's `.gitignore`.