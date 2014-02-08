---
layout: post
title:  "Scrolling background windows in Xfce"
date:   2012-10-18 12:01:01
comments: true
categories: discoveries
tags: linux xfce xubuntu
---

I recently found that I was lacking this feature in my Xubuntu 12.04. I remember once having this on by default in KDE, so I wanted to find out how to do this in Xfce.

So this is what you need to do to enable background sccrolling in Xfce (in a terminal):

```
$ xfconf-query -c xfwm4 -p /general/raise_with_any_button -s false
```

Another way is to open Xfce Setting editor and navigate to `xfwm4 -> general -> raise_with_any_button -> false`

Kudos to [Will Santos](http://www.blogger.com/profile/11297217775847303000) for his [blog post](http://xubuntugeek.blogspot.com/2012/05/mouse-scrolling-without-raising-window.html).