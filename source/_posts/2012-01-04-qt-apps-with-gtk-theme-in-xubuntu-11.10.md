---
layout: post
title:  "Qt apps with GTK theme in Xubuntu 11.10"
date:   2012-01-04 12:01:01
comments: true
categories: discoveries
tags: linux xfce qt xubuntu
---


As you may have noticed, Qt apps no longer use GTK+ theme in Xubuntu 11.10. For me this became particularly noticeable in Psi+.
The problem is caused by QGtkStyle, which cannot find GTK+ theme since Xfce stores it in an unusual location (not sure why 11.04 could find it though).

To fix the problem add the following to `~/.config/xfce4/gtkrc` (create the file if it does not exist):

```
gtk-theme-name = greybird # Change 'greybird' to whatever Xfce theme you're using
```

Create `~/.config/xfce4/xinitrc` and add the following to it:

```
#!/bin/sh
GTK2_RC_FILES=$HOME/.config/xfce4/gtkrc
export GTK2_RC_FILES
. /etc/xdg/xfce4/xinitrc
```

After relogin all Qt apps will use your current Xfce GTK+ theme.