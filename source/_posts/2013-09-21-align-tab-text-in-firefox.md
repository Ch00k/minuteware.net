---
layout: post
title:  "Align tab text in Firefox"
date:   2013-09-21 12:01:01
comments: true
categories: discoveries
tags: firefox
---

Linux Mint uses it’s customized Firefox theme which has tabs text centered. This is not something you’d want if you are using Tree Style Tab extension. This can be overridden though. In your Firefox profile directory (which should be `~/.mozilla/firefox/<some_random_chars>.default`) create a subdirectory called chrome and then create a file userChrome.css in this chrome subdirectory with the following content:

```css	
.tab-text {
  text-align: left !important;
}
```

Restart Firefox and you’re done – tabs text is aligned left.